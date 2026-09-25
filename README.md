# SHAMMAH MISSION PORTAL
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SHAMMAH MISSION SCHOOL PORTAL</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:Arial, sans-serif;
}

body{
    min-height:100vh;
    background:linear-gradient(135deg,#0b5d1e,#178b32,#e9f7ec);
    display:flex;
    justify-content:center;
    align-items:center;
    padding:20px;
}

.container{
    width:100%;
    max-width:430px;
    background:white;
    border-radius:22px;
    padding:28px 22px;
    box-shadow:0 15px 40px rgba(0,0,0,.25);
    text-align:center;
}

.logo{
    width:100px;
    height:100px;
    border-radius:50%;
    object-fit:contain;
    margin:auto;
    display:block;
    border:4px solid #0b5d1e;
    padding:5px;
}

h1{
    color:#0b5d1e;
    margin-top:15px;
    font-size:25px;
}

.portal{
    color:#d4a017;
    font-size:22px;
    font-weight:bold;
    margin-top:5px;
}

.subtitle{
    color:#666;
    margin:10px 0 22px;
}

.roles{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:12px;
    margin-bottom:20px;
}

.role-btn{
    border:none;
    border-radius:14px;
    padding:18px 8px;
    background:#f1f7f2;
    color:#0b5d1e;
    font-weight:bold;
    cursor:pointer;
    font-size:16px;
    border:2px solid #d8eadb;
    transition:.2s;
}

.role-btn:hover{
    background:#dff1e2;
}

.role-btn.active{
    background:#0b5d1e;
    color:white;
    border-color:#0b5d1e;
}

.login-box{
    display:none;
    text-align:left;
}

.login-box.show{
    display:block;
}

.login-title{
    text-align:center;
    color:#0b5d1e;
    margin-bottom:15px;
    font-size:19px;
    font-weight:bold;
}

label{
    display:block;
    margin-top:12px;
    margin-bottom:5px;
    font-weight:bold;
    color:#333;
}

input{
    width:100%;
    padding:13px;
    border:1px solid #ccc;
    border-radius:10px;
    font-size:16px;
}

.login-btn{
    width:100%;
    margin-top:20px;
    padding:14px;
    border:none;
    border-radius:10px;
    background:#0b5d1e;
    color:white;
    font-size:17px;
    font-weight:bold;
    cursor:pointer;
}

.login-btn:hover{
    background:#084a17;
}

.message{
    text-align:center;
    margin-top:12px;
    color:#c62828;
    font-weight:bold;
    min-height:20px;
}

.footer{
    margin-top:20px;
    font-size:12px;
    color:#777;
}
</style>
</head>

<body>

<div class="container">

    <!-- LOGO -->
    <img
        class="logo"
        id="schoolLogo"
        src=""
        alt="School Logo"
        onerror="this.style.display='none';"
    >

    <h1>SHAMMAH MISSION SCHOOL</h1>
    <div class="portal">PORTAL</div>

    <div class="subtitle">
        Results Management System
    </div>

    <!-- ROLE SELECTION -->
    <div class="roles">

        <button
            type="button"
            class="role-btn"
            id="directorRole"
            onclick="selectRole('director')">
            👨‍💼<br>
            DIRECTOR / ADMIN
        </button>

        <button
            type="button"
            class="role-btn"
            id="teacherRole"
            onclick="selectRole('teacher')">
            👨‍🏫<br>
            TEACHER
        </button>

    </div>

    <!-- LOGIN -->
    <div class="login-box" id="loginBox">

        <div class="login-title" id="loginTitle">
            Login
        </div>

        <label>Username</label>
        <input
            type="text"
            id="username"
            placeholder="Enter username"
            autocomplete="username"
        >

        <label>Password</label>
        <input
            type="password"
            id="password"
            placeholder="Enter password"
            autocomplete="current-password"
        >

        <button
            type="button"
            class="login-btn"
            onclick="login()">
            LOGIN
        </button>

        <div class="message" id="message"></div>

    </div>

    <div class="footer">
        SHAMMAH MISSION SCHOOL • Marakwet West, Kapsowar
    </div>

</div>

<script>

const DB_KEY = "SHAMMAH_MISSION_SCHOOL_DATABASE";

let selectedRole = "";

function createDatabase(){

    let db = localStorage.getItem(DB_KEY);

    if(db){
        return JSON.parse(db);
    }

    const database = {

        school:{
            name:"SHAMMAH MISSION SCHOOL",
            portalName:"SHAMMAH MISSION SCHOOL PORTAL",
            UPI:"",
            email:"aicshammahschool2025@gmail.com",
            location:"Marakwet West, Kapsowar",
            logo:"",
            openingDate:"",
            closingDate:""
        },

        users:[
            {
                username:"admin",
                password:"admin123",
                role:"director",
                name:"Director"
            },
            {
                username:"teacher",
                password:"teacher123",
                role:"teacher",
                name:"Mr Kim"
            }
        ],

        classes:[
            "Grade 7",
            "Grade 8",
            "Grade 9"
        ],

        subjects:[
            "Agriculture",
            "Integrated Science",
            "Mathematics",
            "English",
            "Kiswahili",
            "SST",
            "CRE",
            "Pre/Tech",
            "C/A"
        ],

        teachers:[
            {
                name:"Mr Kim",
                phone:"",
                allocations:[
                    "Agriculture Grade 7",
                    "Agriculture Grade 8",
                    "Agriculture Grade 9",
                    "Pre/Tech Grade 7",
                    "Integrated Science Grade 7",
                    "Integrated Science Grade 8"
                ]
            },

            {
                name:"Md Keziah",
                phone:"",
                allocations:[
                    "Mathematics Grade 7",
                    "Mathematics Grade 8",
                    "Mathematics Grade 9",
                    "CRE Grade 7",
                    "CRE Grade 8",
                    "Integrated Science Grade 9"
                ]
            },

            {
                name:"Mr Collin's",
                phone:"",
                allocations:[
                    "English Grade 7",
                    "English Grade 8",
                    "English Grade 9",
                    "Pre/Tech Grade 8",
                    "Pre/Tech Grade 9",
                    "CRE Grade 9"
                ]
            },

            {
                name:"Mr Jonah",
                phone:"",
                allocations:[
                    "Kiswahili Grade 7",
                    "Kiswahili Grade 8",
                    "Kiswahili Grade 9",
                    "SST Grade 7",
                    "SST Grade 8",
                    "SST Grade 9"
                ]
            },

            {
                name:"Mr Kanda",
                phone:"",
                allocations:[
                    "C/A Grade 7",
                    "C/A Grade 8",
                    "C/A Grade 9"
                ]
            }
        ],

        students:[],
        results:[],

        grading:{
            EE:{
                min:820
            },
            ME:{
                min:450,
                max:819
            },
            AE:{
                min:250,
                max:449
            },
            BE:{
                min:0,
                max:249
            }
        },

        currentAcademicYear:"2026",
        currentTerm:"Term 1"
    };

    localStorage.setItem(DB_KEY,JSON.stringify(database));

    return database;
}


function selectRole(role){

    selectedRole = role;

    document.getElementById("directorRole")
        .classList.remove("active");

    document.getElementById("teacherRole")
        .classList.remove("active");

    if(role === "director"){

        document.getElementById("directorRole")
            .classList.add("active");

        document.getElementById("loginTitle")
            .textContent = "DIRECTOR / ADMIN LOGIN";

    }

    if(role === "teacher"){

        document.getElementById("teacherRole")
            .classList.add("active");

        document.getElementById("loginTitle")
            .textContent = "TEACHER LOGIN";

    }

    document.getElementById("loginBox")
        .classList.add("show");

    document.getElementById("message")
        .textContent = "";

    document.getElementById("username").focus();
}


function login(){

    const username =
        document.getElementById("username").value.trim();

    const password =
        document.getElementById("password").value;

    const message =
        document.getElementById("message");

    if(!selectedRole){

        message.textContent =
            "Please select Director/Admin or Teacher.";

        return;
    }

    if(!username || !password){

        message.textContent =
            "Please enter username
