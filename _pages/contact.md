---
layout: single
permalink: /contact
title: "Contact"
---

# Contact

<br/>
<br/>

<form id="contact_form" class="contact_form" action="https://152.67.217.36:5000/submit_form" method="POST">
  <div class="input_container">
    <input type="text" name="name" placeholder="Name" required/>
    <input type="email" name="email" placeholder="Email" required/>
  </div>
  <br />
  <textarea name="message" placeholder="Message" maxlength="500" required></textarea>
  <button type="submit">Submit</button>
</form>
