# create-report.php
I need help with the code. The image managed to be uploaded in database but not in the folder.

<?php
session_start();
//echo $_SESSION['id'];
//$_SESSION['msg'];
include("dbconnection.php");
include("checklogin.php");
check_login();

if(isset($_POST['send']))
{
  
    $email=$_SESSION['login'];
    $name=$_POST['name'];
    $contactno=$_POST['contactno'];
    $subject=$_POST['subject'];
    $location=$_POST['location'];
    $incident_date=$_POST['incident_date'];
    $incident_time=$_POST['incident_time'];
    $report=$_POST['description'];
    $st="Open";
    $pdate=date('Y-m-d');

    $filename=$_FILES['image']['name'];
    $filetmpname=$_FILES['image']['tmp_name'];
    $folder='assets/report/';


    move_uploaded_file($filetmpname, $folder.$filename);

    $a=mysqli_query($con,"insert into report(report_id,email_id,name,contactno,subject,location,incident_date,incident_time,report,image,status,posting_date)  values
    ('$rid','$email','$name','$contactno','$subject','$location','$incident_date','$incident_time',
    '$report','$filename','$st','$pdate')");
        
        if($a)
        {
            echo "<script>alert('Report Submitted'); location.replace(document.referrer)</script>";
       }
        }
       
?>

<!DOCTYPE html>
<html>
<head>
<meta http-equiv="content-type" content="text/html;charset=UTF-8" />
<meta charset="utf-8" />
<title>Paddy Monitoring System | Create Report</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
<meta content="" name="description" />
<meta content="" name="author" />

<link href="assets/plugins/pace/pace-theme-flash.css" rel="stylesheet" type="text/css" media="screen"/>
<link href="assets/plugins/boostrapv3/css/bootstrap.min.css" rel="stylesheet" type="text/css"/>
<link href="assets/plugins/boostrapv3/css/bootstrap-theme.min.css" rel="stylesheet" type="text/css"/>
<link href="assets/plugins/font-awesome/css/font-awesome.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/animate.min.css" rel="stylesheet" type="text/css"/>
<link href="assets/plugins/jquery-scrollbar/jquery.scrollbar.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/style.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/responsive.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/custom-icon-set.css" rel="stylesheet" type="text/css"/>


</head>
<body class="">
<?php include("header.php");?>
<div class="page-container row-fluid">	
	<?php include("leftbar.php");?>
	<div class="clearfix"></div>
    <!-- END SIDEBAR MENU --> 
  </div>
  </div>
  <!-- END SIDEBAR --> 
  <!-- BEGIN PAGE CONTAINER-->
  <div class="page-content"> 
    <!-- BEGIN SAMPLE PORTLET CONFIGURATION MODAL FORM-->
    <div id="portlet-config" class="modal hide">
      <div class="modal-header">
        <button data-dismiss="modal" class="close" type="button"></button>
        <h3>Widget Settings</h3>
      </div>
      <div class="modal-body"> Widget settings form goes here </div>
    </div>
    <div class="clearfix"></div>
    <div class="content">  
		<div class="page-title">	
			<h3>Create report</h3>
             <div class="row">
                        <div class="col-md-12">
                            
                            <form class="form-horizontal" name="form1" method="post" action="" onSubmit="return valid();" enctype="multipart/form-data">
                            <div class="panel panel-default">
                            </div>  
                                <div class="panel-body bg-white">      
                                <?php if(isset($_SESSION['msg1'])): ?>                                                                  
                                    <p align="center" style="color:#FF0000"><?=$_SESSION['msg1'];?><?=$_SESSION['msg1']="";?></p>
                                    <?php endif; ?>
                                    <div class="form-group">
                                        <label class="col-md-3 col-xs-12 control-label">Farmer Name </label>
                                        <div class="col-md-6 col-xs-12">                                             
                                        <div class="input-group">
                                        <span class="input-group-addon"><span class="fa fa-pencil"></span></span>
                                                <input type="text" name="name" id="name" value="" required class="form-control"/>
                                            </div>                                            
                                                                                    
                                            </div>
                                        </div>
                                                                                
                                              <div class="form-group">                                        
                                        <label class="col-md-3 col-xs-12 control-label">Farmer Contact No</label>
                                        <div class="col-md-6 col-xs-12"> 
                                            <div class="input-group">
                                                <span class="input-group-addon"><span class="fa fa-pencil"></span></span>
                                                <input type="text" name="contactno" id="contactno" value="" required class="form-control"/>
                                            </div>            
                                         </div>
                                    </div>
                                    
                                    <div class="form-group">                                        
                                        <label class="col-md-3 col-xs-12 control-label">Subject</label>
                                        <div class="col-md-9 col-xs-12">
                                            <div class="input-group">
                                                <span class="input-group-addon"><span class="fa fa-pencil"></span></span>
                                                <input type="text" name="subject" id="subject" value="" required class="form-control"/>
                                            </div>            
                                         </div>
                                    </div>

                                    <div class="form-group">
                                        <label class="col-md-3 col-xs-12 control-label">Field Location</label>
                                        <div class="col-md-9 col-xs-12">      
                                        <div class="input-group">         
                                        <span class="input-group-addon"><span class="fa fa-pencil"></span></span>       
                                        <input type="text" name="location" id="location" value="" required class="form-control"/>
                                          </div>
                                        </div>  
                                        </div>  
                                                            
                                                                            
                                            <div class="form-group">
                                    <label class="col-md-3 col-xs-12 control-label">Incident Date</label>
                                    <div class="col-md-3 col-xs-12">
                                    <div class="input-group">
                                        <span class="input-group-addon"><span class="fa fa-pencil"></span></span>
                                        <input type="date" name="incident_date" class="form-control datepicker" value="" required>
                                </div>
                                    </div>

                                    </div>  
                                    <div class="form-group">
                                    <label class="col-md-3 col-xs-12 control-label">Incident Time</label>
                                    <div class="col-md-3 col-xs-12">
                                    <div class="input-group">
                                        <span class="input-group-addon"><span class="fa fa-pencil"></span></span>
                                        <input type="time" name="incident_time" class="form-control datepicker" value="" required>
                                </div>
                                    </div>
                                    </div>
                                     		  
                                    <div class="form-group">
                                        <label class="col-md-3 col-xs-12 control-label">Brief Description</label>
                                        <div class="col-md-9 col-xs-12">    
                                         <textarea name="description" required class="form-control" rows="2"></textarea>
                                            
                                        </div>
                                        </div>  
                                    <div class="form-group">
                                    <label class="col-md-3 col-xs-12 control-label">Attach Image</label>
                                    <div class="col-md-3 col-xs-12">
                                    <input type="file" name="image" class="form-control" required >
                                </div>
                                    </div>
                                   
                                    </div>
                                    
                                </div>
                                </div>
                                <div class="panel-footer">
                                    <button class="btn btn-default">Clear Form</button>                                    
                                    <input type="submit" value="Send" name="send" class="btn btn-primary pull-right">
                                </div>
                            </div>
                            </form>
                            
                        </div>
                    </div>                    
            	
		</div>
    </div>
  </div>

 </div>
<script src="assets/plugins/jquery-1.8.3.min.js" type="text/javascript"></script> 
<script src="assets/plugins/jquery-ui/jquery-ui-1.10.1.custom.min.js" type="text/javascript"></script> 
<script src="assets/plugins/bootstrap/js/bootstrap.min.js" type="text/javascript"></script> 
<script src="assets/plugins/breakpoints.js" type="text/javascript"></script> 
<script src="assets/plugins/jquery-unveil/jquery.unveil.min.js" type="text/javascript"></script> 
<script src="assets/plugins/jquery-block-ui/jqueryblockui.js" type="text/javascript"></script> 
<script src="assets/plugins/jquery-scrollbar/jquery.scrollbar.min.js" type="text/javascript"></script>
<script src="assets/plugins/pace/pace.min.js" type="text/javascript"></script>  
<script src="assets/plugins/jquery-numberAnimate/jquery.animateNumbers.js" type="text/javascript"></script>
<script src="assets/js/core.js" type="text/javascript"></script> 
<script src="assets/js/chat.js" type="text/javascript"></script> 
<script src="assets/js/demo.js" type="text/javascript"></script> 
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.14.7/dist/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>

</body>
</html>
