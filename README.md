# codeigniter-ckeditor-kcfinder
[Codeigniter](http://codeigniter.com/) with [CKEDITOR](http://ckeditor.com/) and [KCFINDER](http://kcfinder.sunhater.com/) using session for authenctication

# Setup
Download [Codeigniter](http://codeigniter.com/) , [CKEDITOR](http://ckeditor.com/) , [KCFINDER](http://kcfinder.sunhater.com/) master file

Put [CKEDITOR](http://ckeditor.com/) , [KCFINDER](http://kcfinder.sunhater.com/) in your [Codeigniter](http://codeigniter.com/) files. For the example, i create assets directory.

# Config 1
open your index.php CI file on root directory and modify  some line
```
$application_folder = 'application';
```
to
```
$application_folder = dirname(__FILE__) . DIRECTORY_SEPARATOR . 'application';
```

and another line
```
$system_path = 'system';
```
to
```
$system_path = dirname(__FILE__) . DIRECTORY_SEPARATOR . 'system';
```

# Config 2
give authentication to access kcfinder for security. i use session for this.
open ```kcfinder->conf directory``` and open ```config.php```

and then get session from CI with this code ( i set session with named upload_image_file_manager to access filemanager )
```
ob_start();
include('../../../../index.php');
ob_end_clean();
$CI =& get_instance();
$CI->load->driver('session');
if(@$_SESSION['upload_image_file_manager'] == TRUE){
	$codeigniterAuth = true;
} else {
	$codeigniterAuth = false;
}
```

modify general setting from kcfinder like this
```
'disabled' => $codeigniterAuth,
```

so we can conclude that we must have session named ```upload_image_file_manager``` to access kcfinder

# Config 4
and to using ckeditor & kcfinder we can include the ckeditor.js
```
<script src="<?php echo base_url('assets/ckeditor/ckeditor.js'); ?>"></script>
```
and replace ```filebrowserImageBrowseUrl```
```
 CKEDITOR.replace('editor1' ,{
		filebrowserImageBrowseUrl : '<?php echo base_url('assets/kcfinder');?>'
	});
```

# Let's try
for the example i create two page. first without session so when we access the upload manager we will get notification that we not authorized to access it.
and the second i give session named upload_image_file_manager so when we do the step before we can access kcfinder like upload files and take it to ckeditor textarea
