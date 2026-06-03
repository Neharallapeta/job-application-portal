<!DOCTYPE html>
<html>
<head>
<title>Job Application Portal</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<div class="container">

<h1>Software Developer</h1>

<p><b>Company:</b> Demo Technologies Pvt Ltd</p>
<p><b>Location:</b> Hyderabad</p>
<p><b>Experience:</b> 0-2 Years</p>
<p><b>Skills:</b> Java, SQL, HTML, CSS</p>

<h2>Apply Now</h2>

<input id="fullName" placeholder="Full Name">

<input id="email" placeholder="Email">

<input id="phoneNumber" placeholder="Phone Number">

<input id="qualification" placeholder="Qualification">

<input id="experience" placeholder="Experience">

<input id="skills" placeholder="Skills">

<textarea id="coverLetter"
placeholder="Cover Letter">
</textarea>

<button onclick="applyJob()">
Apply Now
</button>

<p id="result"></p>

</div>

<script src="script.js"></script>

</body>
</html>
body{
font-family:Arial;
padding:20px;
}

.container{
max-width:700px;
margin:auto;
}

input,textarea{
width:100%;
padding:10px;
margin:10px 0;
}

button{
padding:10px 20px;
cursor:pointer;
}
async function applyJob() {

    const data = {
        fullName: document.getElementById("fullName").value,
        email: document.getElementById("email").value,
        phoneNumber: document.getElementById("phoneNumber").value,
        qualification: document.getElementById("qualification").value,
        experience: document.getElementById("experience").value,
        skills: document.getElementById("skills").value,
        coverLetter: document.getElementById("coverLetter").value
    };

    try {

        const response = await fetch(
            "https://v17cq7iiab.execute-api.ap-south-1.amazonaws.com/prod/apply",
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(data)
            }
        );

        const result = await response.json();

        console.log(result);

        if (result.body) {
            const bodyData = JSON.parse(result.body);
            document.getElementById("result").innerHTML =
                bodyData.message;
        } else {
            document.getElementById("result").innerHTML =
                result.message;
        }

    } catch (error) {

        console.error(error);

        document.getElementById("result").innerHTML =
            "Application submission failed";
    }
}
