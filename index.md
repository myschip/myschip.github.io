### Welcome to Dynamic IP Updater for ISPConfig Server.
This IP Updater is designed and created especially for those who is using dynamic IP for their ISPConfig Server instead of static IP as usually required. When it is setup using cron job as described in the how to guids below, the IP Updater will update the dynamic IP and resync it accordingly.

### How To Guides #1
Firstly, you will need to copy resync.php to ipu_resync.php and app.inc.php to ipu_app.inc.php. In ubuntu-based server, to copy the files to new names, basically just type:  
sudo cp /usr/local/ispconfig/interface/web/tools/resync.php /usr/local/ispconfig/interface/web/tools/ipu_resync.php  
sudo cp /usr/local/ispconfig/interface/lib/app.inc.php /usr/local/ispconfig/interface/lib/ipu_app.inc.php

### How To Guides #2
Secondly, in the newly copied file - ipu_resync.php, change require_once from app.inc.php to ipu_app.inc.php, and disable admin check and tpl by commenting out the lines, as follows:  
require_once '../../lib/ipu_app.inc.php';  
...  
//* Check permissions for module  
// $app->auth->check_module_permissions('admin');  
...  
//* This is only allowed for administrators  
// if(!$app->auth->is_admin()) die('only allowed for administrators.');  
...  
// $app->tpl->setVar('msg', $msg);  
// $app->tpl->setVar('error', $error);  
...  
// $app->tpl_defaults();  
// $app->tpl->pparse();

### How To Guides #3
Thirdly, in the other newly copied file - ipu_app.inc.php, disable start_session() by commenting out the line as follows:
// session_start();

### How To Guides #4
Fourthly, create ip_updater.php file in /usr/local/ispconfig/interface/web/tools/ and paste ip_updater.php code to it or use wget as follows:  
sudo cd /usr/local/ispconfig/interface/web/tools  
sudo wget https://raw.githubusercontent.com/ahrasis/IP_Updater/master/ip_updater.php

### How To Guides #5
Firthly, in the other newly copied file - ipu_app.inc.php, disable start_session() by commenting out the line as follows:  
// session_start();

### How To Guides #6
Create cron job using sudo crontab -e or ISPConfig control panel. The timing is up to you but I would suggest to add one at every reboot and the other, every hour on selected minute e.g.:  
@reboot php -q /usr/local/ispconfig/interface/web/tools/ip_updater.php  
18 * * * * php -q /usr/local/ispconfig/interface/web/tools/ip_updater.php

### License
As stated in the ip_updater.php file. Feel free to fork the code and improvise it to suit your needs accordingly.