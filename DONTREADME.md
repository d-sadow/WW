# WW
Веб студия Тюмень
<?php
    include ('../../../include/basic_file.php'); 
    $status = $_POST['status']; $term = $_POST['term'];
    $searchTopicTask = formatting($_POST['searchTopicTask']); $searchTopicTaskTo = formatting($_POST['searchTopicTaskTo']);
    
    if($term == '0'){$request = "AND termDate = '{$current_date}'";}
    elseif($term == '1'){$request = "AND termDate = '{$tomorrow_date}'";}
    elseif($term == '2'){$newDate = date('Y-m-d', time() + 172800); $request = "AND termDate = '{$newDate}'";}
    elseif($term == '3'){$newDate = date('Y-m-d', time() + 259200); $request = "AND termDate = '{$newDate}'";}
    elseif($term == '4'){$newDate = date('Y-m-d', time() + 345600); $request = "AND termDate = '{$newDate}'";}
    elseif($term == '5'){$newDate = date('Y-m-d', time() + 432000); $request = "AND termDate = '{$newDate}'";}
    elseif($term == '-1'){$request = "AND termDate < '{$current_date}'";}
    else{$request = null;}
    
    if((int)$status){$requestStatus = "status = '{$status}' AND substatus != '99' AND addUser = '{$_SESSION['user_id']}'";}
    elseif($status == 'privateA'){$requestStatus = "status = '{$_SESSION['user_id']}' AND substatus = '99' AND addUser = '{$_SESSION['user_id']}'";}
    elseif($status == 'inboxA'){$requestStatus = "status = '{$_SESSION['user_id']}' AND substatus = '99' AND addUser != '{$_SESSION['user_id']}'";}
    elseif($status == 'outboxA'){$requestStatus = "status != '{$_SESSION['user_id']}' AND substatus = '99' AND addUser = '{$_SESSION['user_id']}'";}
    elseif($status == 'all'){$requestStatus = "status != '{$_SESSION['user_id']}' AND substatus != '99' AND addUser = '{$_SESSION['user_id']}'";}
    else {$requestStatus = "status = '{$_SESSION['user_id']}' AND substatus != '99'";}
    
    if($searchTopicTask){$requestSearchTopic = "AND topic LIKE '%{$searchTopicTask}%'";}
    if($searchTopicTaskTo){$requestSearchTopic = "AND topic LIKE '%{$searchTopicTaskTo}%'";}
    
    if($term == '9')
    {
        $requestStatus = "status != '{$_SESSION['user_id']}' AND substatus != '99' AND addUser = '{$_SESSION['user_id']}'"; 
        $request = "AND termDate < '{$current_date}' AND addUser = '{$_SESSION['user_id']}'";
    }
    if($term == '10')
    {
        $requestStatus = "status != '{$_SESSION['user_id']}' AND substatus != '99' AND addUser = '{$_SESSION['user_id']}'"; 
        $request = null;
    }
    if($term == '11')
    {
        $requestStatus = "status != '{$_SESSION['user_id']}' AND substatus = '98' AND addUser = '{$_SESSION['user_id']}'"; 
        $request = null;
    }
?>