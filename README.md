Short-Code-
===========

/* GET COLUMN NAMES OF TABLE */
 	$result = mysql_query("SHOW COLUMNS FROM tbl_property");
	
	$up_prop_id=$_REQUEST['edit_property_id'];
	
      if (!$result) {
        echo 'Could not run query: ' . mysql_error();
      }
      $fieldnames=array();
      if (mysql_num_rows($result) > 0) {
        while ($row = mysql_fetch_assoc($result)) {
          $fieldnames[] = $row['Field'];
        }
      }
	  
	  if(empty($_REQUEST['edit_property_id']))
	  {
	  /* COMPARING COLUMN NAME WITH FORM FIELDS FOR INSERT */
	  
	  $cnt=count($fieldnames);
	  $form_val=$_REQUEST;
	  $column="";
	  $val="";
	  for($i=0;$i<$cnt;$i++)
	  {
		  if(array_key_exists($fieldnames[$i],$form_val))
		  {
			  
			  /*Arranging columns*/
			  $column.=$fieldnames[$i];
			  if($i!=$cnt-1)
			  $column.=",";
			  
			  /*Arranging values*/
			  $value=$form_val[$fieldnames[$i]];
			  $val.="'$value'";
			   if($i!=$cnt-1)
			  $val.=",";
		  }
	  }


$sqlmain="insert into tbl_property ($column)values($val)";
	  }
