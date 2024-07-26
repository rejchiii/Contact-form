<script>
  import Alert from "../public/Alert.svelte";

  let valid = false;
  let selectedValue = null;
  let checkbox = false;
  let errors = {FirstName:'', LastName:'', Email:'', Query:'', Message:'', checkbox:'', selectedValue:''}

  let showAlert = false;
  let alertMessage = '';
  let alertType = 'info';

  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;


  $:email = '';
   let  LastName = "";
   let  FirstName = "";
  $:message='';

  const SubmitHandler = () => {
    valid = true;
    if (selectedValue === null) {
      errors.selectedValue = "Please select a query type";
      valid = false;
    } else {
      errors.selectedValue = "";
      valid = true;
    }
    if (!checkbox) {
      errors.checkbox = "To submit this form, please consent to being contacted";
      valid = false;
    } else {
      errors.checkbox = "";
      valid = true;
    }
    if (message === '') {
      errors.Message = "This field is required";
      valid = false;
    } else {
      errors.Message = "";
  }
  if (!emailPattern.test(email)) {
  
    errors.Email = "Please enter a valid email address";
    valid = false;
      } else {
        errors.Email = "";     
  }
  if (LastName === '') {
    errors.LastName = "This field is required";
    valid = false;
  }
  else {
    errors.LastName = "";
  }
  if (FirstName === '') {
    errors.FirstName = "This field is required";
    valid = false;
  }
  else {
    errors.FirstName = "";
  }
  console.log(FirstName, LastName)
  if (valid){
    showAlert = true;
    setTimeout(()=> {
      showAlert = false;
    }, 5000);

  };
  
};
  


  function handleRadioChange(event) {
      selectedValue = event.target.value;
  }
  
  function handleCheckboxChange(event) {
      checkbox = event.target.checked;
  };
 
  
</script>


<main class="main">
  <div class="container">
    <div class="form-group" style="margin-left: 50px;">
    {#if showAlert}
    <Alert> <p>{message}</p></Alert>
    {/if}
    </div>
    <div class="card">
      <form on:submit|preventDefault={SubmitHandler}>
        <p style="user-select:none">Contact Us</p>
        <div class="form-group">
          <label for="first_name" class="label left">First Name<span class="blue span-space">*</span></label>
          <label for="last_name" class="label right">Last Name<span class="blue span-space">*</span></label>
        </div>

        <div class="input-group">
          <input type="text" class="input {errors.FirstName ? 'error-border' : ''}" id="FirstName" name="first_name" bind:value={FirstName}>
          <input type="text" class="input {errors.LastName ? 'error-border' : ''}" id="LastName" name="last_name" bind:value={LastName}>
        </div>
        <div class="errors" style="margin-top: 5px;">{errors.FirstName}</div>
        <div class="errors form-group" style="margin-top: 5px; margin-left:260px; white-space:nowrap">{errors.LastName}</div>
  
        <div class="form-group">
          <label for="email" class="label left">Email Address<span class="blue span-space" id="Email">*</span></label>
        </div>

        <div class="input-group">
          <input type="text" class="input {errors.Email ? 'error-border' : ''}" id="email" name="email" style="width: 195%;" bind:value={email}>
        </div>
        <div class="errors" style="margin-top:5px">{errors.Email}</div>

        <div class="form-group">
          <label for="" class="label left">Query type<span class="blue span-space">*</span></label>
        </div>
        
        <div class="button-container">
          <label class="custom-radio {selectedValue === '1' ? 'checked' : ''}">
            <input
              type="radio"
              name="group"
              value="1"
              on:change={handleRadioChange}
            />
            <div class="circle-container">
              <div class="circle"></div>
              <span>General Enquiry</span>
            </div>
          </label>
      
          <label class="custom-radio {selectedValue === '2' ? 'checked' : ''}">
            <input
              type="radio"
              name="group"
              value="2"
              on:change={handleRadioChange}
            />
            <div class="circle-container">
              <div class="circle"></div>
              <span>Support Request</span>
            </div>
          </label>
        </div>
        
        <div class="errors" style="margin-top: 5px;"><label for="">{errors.selectedValue}</label></div>
        
        <div class="form-group">
          <label for="message" class="label left" >Message<span class="blue span-space">*</span></label>
        </div>             
        <div class="input-group">
          <textarea class="textarea {errors.Message ? 'error-border':''}" id="message" name="message" bind:value={message}></textarea>
        </div>
        <div class="errors" style="margin-top: 10px;">{errors.Message}</div>

        <div class="checkbox-container">
          <input type="checkbox" id="heckbox" name="Checkbox" class="checkbox" on:change={handleCheckboxChange} />
          <div class="custom-checkbox"></div>
          <label for="Checkbox" class="checkbox-label">I consent to being contacted by the team<span class="span-space blue">*</span></label>
        </div> 
        <div class="errors" style="margin-top: 45px;"><label for="Checkbox" >{errors.checkbox} </label></div>

        <div class="form-group">
          <input type="submit" value="Submit" class="submit-button">
        </div>          
      </form>
    </div>
  </div>
</main>


<style>
  .card {
    position: relative;
    width: 500px;
    height: 650px;
    background: rgb(255, 255, 255);
    padding: 20px;
    border-radius: 10px;
  }
  
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh; 
    padding: 20px; 
    box-sizing: border-box;
  }

  p {
    font-family: Karla;
    font-size: 23px;
    margin: 5px;
    font-weight: 700;
  }
  
  .label {
    font-family: Karla;
    font-size: 16px;
    font-weight: 400 !important;
    margin: 2px;
    margin-top: 20px;
    margin-bottom: 10px;
    color: hsl(187, 24%, 22%);
    user-select: none;
  }

  .form-group {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px; 
    margin-top: 10px;
  }
  
  .blue {
    color: hsl(169, 82%, 27%);
  }
  
  .input-group {
    margin: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 10px;
  }
  
  .input {
    font-family: Karla; 
    font-size: 16px;
    background: white;
    border: 2px solid hsl(186, 15%, 59%);
    padding: 10px;
    border-radius: 6px;
    transition: border-color 0.3s ease;  
  }
  
  .input:focus {
    border: 2px solid hsl(169, 82%, 27%);
    outline: none;
  }
  
  .span-space {
    margin-left: 5px;
  }

  .button-container {
    display: flex;
    gap: 10px; 
  }
  
  .custom-radio {
    width: 100%;
    display: inline-flex;
    align-items: center;
    padding: 10px;
    border: 2px solid hsl(186, 15%, 59%);
    border-radius: 6px;
    background-color: white;
    cursor: pointer;
    font-size: 16px;
    font-family: Karla;
    position: relative;
    user-select: none;
  }
  
  .custom-radio input[type="radio"] {
    position: absolute;
    left: -9999px; 
  }
  
  .circle-container {
    display: flex;
    align-items: center;
    position: relative;
  }
  
  .circle {
    width: 15px;
    height: 15px;
    border: 2px solid #ccc;
    border-radius: 50%;
    background-color: white;
    margin-right: 10px; 
    position: relative;
  }
  
  .custom-radio input[type="radio"]:checked + .circle-container .circle {
    border-color: white;
  }
  
  .custom-radio input[type="radio"]:checked + .circle-container .circle::after {
    content: url('./assets/icon-radio-selected.svg'); 
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 20px;
    height: 20px;
  }
  
  .custom-radio.checked {
    background-color: hsl(148, 38%, 91%); 
    border-color: hsl(169, 82%, 27%);
  }
  
  .custom-radio span {
    display: inline-block;
  }
  
  .custom-radio input[type="radio"]:checked + .circle-container::before {
    content: ''; 
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: hsl(148, 38%, 91%); 
    border-radius: 6px;
    z-index: -1; 
  }

  .textarea {
    width: 205%;
    height: 100px;
    padding: 10px;
    box-sizing: border-box;
    overflow-wrap: break-word;
    white-space: pre-wrap;
    text-align: left;
    resize: none;
    font-family: Karla;
    font-size: 16px;
    background: white;
    border: 2px solid hsl(186, 15%, 59%);
    border-radius: 6px
  }
    .textarea:focus {
  outline: none;
  border: 2px solid hsl(169, 82%, 27%);
  
  
  }   

          .checkbox-container {
              display: flex;
              align-items: center;
              margin: 10px 0;
              position: relative;
          }
  
          
          .checkbox-container input[type="checkbox"] {
            margin-top: 70px;
            position: absolute; 
            opacity: 0; 
            cursor: pointer; 
            width: 100%; 
            height: 200px;
   
          }
  
          
          
          .custom-checkbox {
              margin-top: 80px;
              width: 10px;
              height: 10px;
              background-color: white;
              border: 2px solid hsl(186, 15%, 59%);
              border-radius: 1px;
              cursor: pointer;
              position: absolute;
              
          }
  
          
          .checkbox-container input[type="checkbox"]:checked + .custom-checkbox {
              background-image: url('./assets/icon-checkbox-check.svg');
              background-size: cover;
              width: 15px;
              height: 15px;
              border: none;
              margin-top: 80px;
              position: absolute;
          }
  
          .checkbox-label {
              font-family: Karla;
              font-size: 16px;
              color: hsl(187, 24%, 22%);
              margin-left: 10px;
              margin-top: 80px;
              cursor: pointer;
              position: absolute;
              margin-left: 20px;
              user-select: none;
          }
          .submit-button {
            
            color: white;
            margin-top: 90px;
            width: 205%;
            text-align: center;
            Font-family:Karla; 
            Font-size:16px;
            background:  hsl(169, 82%, 27%);
            border: 1px solid hsl(169, 82%, 27%);
            padding: 15px;
            border-radius: 6px;
            cursor: pointer;
            position:relative;
            
  
          }
          .errors {
            position: absolute;
            color: hsl(0, 66%, 54%);
            font-size: 16px;
            font-family: Karla;
            margin-top: 25px;
            margin-bottom: 0;
            user-select: none;
          }
          .error-border {
            border : 2px solid hsl(0, 66%, 54%);
          }

          </style>