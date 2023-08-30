---
layout: page
title: Sign Up
permalink: /signup/
---
## Hello! 
Thank you for your interest in volunteering for the Grossmont College CVT Echo program!
We are recruiting 7 models for our next event.

(event details go here...)

<div id="count">
    <p>So far, we have signed up <span id="volunteerCount">(loading...)</span> volunteers!</p>
</div>

<form id="volunteerForm" class="recruitForm">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <button type="submit">Sign Up</button>
</form>
<div id="message"></div>

<script src="https://code.jquery.com/jquery-3.7.0.min.js" integrity="sha256-2Pmvv0kuTBOenSvLm6bvfBSSHrUJ+3A7x6P5Ebd07/g=" crossorigin="anonymous"></script>
<script>
    const volunteerCountElement = $('#volunteerCount');
    async function updateVolunteerCount() {
        const url = 'https://script.google.com/macros/s/AKfycbwoTfFf7cq4gkjZfKgBlgG5GnlUMe2grZLD_Ka_yAfZVETyDg5SjHslrOAE5cExZxr5aQ/exec'; // The URL of your deployed volunteer count web app
        try {
            const count = await $.get(url);
            volunteerCountElement.text(count);
        } catch (error) {
            volunteerCountElement.text('Error fetching volunteer count.');
        }
    }
    $(document).ready(function () {
        //style the inputs
        $('#volunteerForm').submit(async function (event) {
        event.preventDefault();
        const name = $('#name').val();
        const email = $('#email').val();
        const url = 'https://script.google.com/macros/s/AKfycbzXmYCuNi5zXs2R3WHBbfTF8zvzjI30PKsnyRQFRmofqJYVy1lL0ByEcA-3_Tqz1ejvuQ/exec'; // The URL of your deployed web app
        try {
            const response = await $.post(url, {
                name: name,
                email: email
            });
            if (response === "Volunteer added successfully.") {
                $('#message').text(response);
                $('#volunteerForm')[0].reset();
                updateVolunteerCount(); // Update the count after successful submission
            } else {
                $('#message').text('Error submitting the form.');
            }
        } catch (error) {
            $('#message').text('Error submitting the form.');
        }
    });
    updateVolunteerCount(); // Update the count when the page loads
});

</script>