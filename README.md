<!DOCTYPE html>

<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KTStudio Login</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Segoe UI,sans-serif;
}

body{
    overflow:hidden;
}

/* VIDEO */

#bgVideo{
    position:fixed;
    top:0;
    left:0;
    width:100%;
    height:100%;
    object-fit:cover;
    z-index:-2;
}

.overlay{
    position:fixed;
    inset:0;
    background:rgba(0,0,0,.65);
    z-index:-1;
}

/* LOGIN BOX */

.container{
    width:100%;
    height:100vh;

    display:flex;
    justify-content:center;
    align-items:center;
}

.box{

    width:420px;

    background:rgba(0,0,0,.75);

    padding:40px;

    border-radius:10px;

    color:white;

    backdrop-filter:blur(8px);
}

.logo{

    text-align:center;

    font-size:40px;

    color:#ff6b00;

    margin-bottom:20px;

    font-weight:bold;
}

.box h2{

    margin-bottom:20px;
}

.box input{

    width:100%;

    padding:14px;

    margin:8px 0;

    border:none;

    border-radius:5px;

    background:#333;

    color:white;
}

.box button{

    width:100%;

    padding:14px;

    margin-top:10px;

    border:none;

    border-radius:5px;

    background:#e50914;

    color:white;

    cursor:pointer;
}

.box button:hover{

    opacity:.9;
}

.link{

    margin-top:15px;

    text-align:center;

    color:#aaa;
}

.link span{

    color:white;

    cursor:pointer;
}

/* REGISTER */

#registerBox{

    display:none;
}

</style>

</head>

<body>

<video autoplay muted loop id="bgVideo">
    <source src="video/login.mp4" type="video/mp4">
</video>

<div class="overlay"></div>

<div class="container">

```
<!-- LOGIN -->

<div class="box" id="loginBox">

    <div class="logo">
        KTStudio
    </div>

    <h2>Đăng nhập</h2>

    <input
        type="text"
        id="loginUser"
        placeholder="Tên đăng nhập">

    <input
        type="password"
        id="loginPass"
        placeholder="Mật khẩu">

    <button onclick="login()">
        Đăng nhập
    </button>

    <div class="link">

        Chưa có tài khoản?

        <span onclick="showRegister()">
            Đăng ký
        </span>

    </div>

</div>

<!-- REGISTER -->

<div class="box" id="registerBox">

    <div class="logo">
        KTStudio
    </div>

    <h2>Đăng ký</h2>

    <input
        type="text"
        id="registerUser"
        placeholder="Tên đăng nhập">

    <input
        type="password"
        id="registerPass"
        placeholder="Mật khẩu">

    <button onclick="registerUser()">
        Đăng ký
    </button>

    <div class="link">

        Đã có tài khoản?

        <span onclick="showLogin()">
            Đăng nhập
        </span>

    </div>

</div>
```

</div>

<script>

function showRegister(){

    document.getElementById("loginBox")
    .style.display="none";

    document.getElementById("registerBox")
    .style.display="block";
}

function showLogin(){

    document.getElementById("registerBox")
    .style.display="none";

    document.getElementById("loginBox")
    .style.display="block";
}

/* ĐĂNG KÝ */

function registerUser(){

    const user =
    document.getElementById("registerUser")
    .value.trim();

    const pass =
    document.getElementById("registerPass")
    .value.trim();

    if(!user || !pass){

        alert("Vui lòng nhập đầy đủ thông tin");
        return;
    }

    let users =
    JSON.parse(
        localStorage.getItem("ktstudio_users")
        || "[]"
    );

    if(
        users.find(
            x => x.username === user
        )
    ){

        alert("Tài khoản đã tồn tại");
        return;
    }

    users.push({

        username:user,
        password:pass

    });

    localStorage.setItem(
        "ktstudio_users",
        JSON.stringify(users)
    );

    alert("Đăng ký thành công");

    showLogin();
}

/* ĐĂNG NHẬP */

function login(){

    const user =
    document.getElementById("loginUser")
    .value.trim();

    const pass =
    document.getElementById("loginPass")
    .value.trim();

    let users =
    JSON.parse(
        localStorage.getItem("ktstudio_users")
        || "[]"
    );

    let account =
    users.find(

        x =>

        x.username === user &&
        x.password === pass

    );

    if(!account){

        alert("Sai tài khoản hoặc mật khẩu");
        return;
    }

    localStorage.setItem(
        "ktstudio_session",
        user
    );

    /* ĐỔI LINK TẠI ĐÂY */

    window.location.href =
    "https://VIET69.BE";
}

</script>

</body>
</html>
