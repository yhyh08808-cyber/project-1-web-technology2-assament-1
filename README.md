<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>نظام تسجيل الطلاب</title>
<style>
body {
    font-family: Arial;
    background: #f4f4f4;
    text-align: center;
}

.container {
    width: 50%;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 10px;
}

input, button {
    width: 90%;
    padding: 10px;
    margin: 5px;
}

button {
    background: green;
    color: white;
    border: none;
}

table {
    width: 100%;
    margin-top: 20px;
    border-collapse: collapse;
}

table, th, td {
    border: 1px solid black;
}

th {
    background: #ddd;
}
</style>
</head>
<body>

<div class="container">
<h2>تسجيل طالب</h2>

<form method="POST">
    <input type="text" name="name" placeholder="اسم الطالب" required><br>
    <input type="email" name="email" placeholder="البريد الإلكتروني" required><br>
    <input type="text" name="id" placeholder="رقم الطالب" required><br>
    <input type="text" name="year" placeholder="سنة الدراسة" required><br>
    <input type="text" name="batch" placeholder="اسم الدفعة" required><br>
    <button type="submit">تسجيل</button>
</form>

<?php
$file = "students.txt";

// حفظ البيانات
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $data = $_POST["name"] . "," .
            $_POST["email"] . "," .
            $_POST["id"] . "," .
            $_POST["year"] . "," .
            $_POST["batch"] . "\n";

    file_put_contents($file, $data, FILE_APPEND);
    echo "<p style='color:green;'>تم التسجيل بنجاح</p>";
}

// عرض البيانات
if (file_exists($file)) {
    $students = file($file);

    echo "<h3>الطلاب المسجلين</h3>";
    echo "<table>";
    echo "<tr>
            <th>الاسم</th>
            <th>البريد</th>
            <th>الرقم</th>
            <th>السنة</th>
            <th>الدفعة</th>
          </tr>";

    foreach ($students as $student) {
        $data = explode(",", trim($student));
        echo "<tr>";
        foreach ($data as $item) {
            echo "<td>$item</td>";
        }
        echo "</tr>";
    }

    echo "</table>";
}
?>

</div>
</body>
</html> 
