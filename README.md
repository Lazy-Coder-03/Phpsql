
 <!DOCTYPE html>
    <head></head>
    <body>
        <h1>Enter CAB details</h1>
        <br>
        <form action = "index.php" method="post">
            <label>C_NO</label>
            <input type = "text" name = "Cno" id = "cn">
            <br>
            <label>Model</label>
            <input type="text" name = "model" id="m">
            <br>
            <label>COLOR</label>
            <input type="text" name = "color" id="clr">
            <br>
            <label>Purchase_date</label>
            <input type="text" name = "p_date" id="pd">
            <br>
            <input type = "submit" name = "submit" value="submit">
        </form>
        <a href="index1.php">See Result</a>
    </body>
</html>

<?php
    //coonection
    $host='localhost';
    $user='root';
    $pass='abc123';

    $conn= new mysqli($host,$user,$pass);
    if($conn->connect_error){
        die("Connection failed:".$conn->connect_error);
    }

    $db="CabAllotmentSystem";
    //select database
    $conn->select_db($db);

    //accepting data from form
    if(isset($_POST['submit'])){
        $Cno=$_POST['Cno'];
        $model=$_POST['model'];
        $color=$_POST['color'];
        $p_date=$_POST['p_date'];
    }

    $sqlinsert="insert into CAB values('$Cno','$model','$color','$p_date')";
    if($conn->query($sqlinsert)==TRUE){
        echo "data inserted successfully";
    }
    else{
        echo "error occured";
    }
    $conn->close();
?>
------------------------------------------
<?php
    $host='localhost';
    $user='root';
    $pass='abc123';
    $conn=new mysqli($host,$user,$pass);
    if($conn->connect_error){
        echo "Connection error";
    }
    $db="CabAllotmentSystem";
    $conn->select_db($db);

    $sqlupdate = "update Cab set color='green' where Cno = 451";
    if($conn->query($sqlupdate)==TRUE){
        echo"DATA:";
    }
    else{
        echo "error";
    }

    $sqldel = "delete from Cab where Cno = 0";

    $sqldisplay="select * from CAB";
    $result=$conn->query($sqldisplay);
    if($result->num_rows>0){
        echo "<table border = 1>";
            echo "<tr>";
                echo "<th>Cno</th>";
                echo "<th>model</th>";''
                echo "<th>color</th>";
                echo "<th>P-date</th>";
            echo "</tr>";

            while($record=$result->fetch_assoc()){
                echo "<tr>";
                    echo"<td>{$record['Cno']}</td>";
                    echo"<td>{$record['model']}</td>";
                    echo"<td>{$record['color']}</td>";
                    echo"<td>{$record['p_date']}</td>";
                     
            }
        echo "</table>";
    }
    else{
        echo "result not found";
    }
$conn->close();

?>
