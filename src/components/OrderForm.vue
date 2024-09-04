<template>
    <div>
      <form @submit.prevent="submitForm">
        <!-- Personal Information -->
        <h3>Personal Information</h3>
        <div>
          <label for="firstName">First Name:</label>
          <input type="text" v-model="form.firstName" id="firstName" required />
        </div>
  
        <div>
          <label for="lastName">Last Name:</label>
          <input type="text" v-model="form.lastName" id="lastName" required />
        </div>
  
        <div>
          <label for="dob">Date of Birth:</label>
          <input type="date" v-model="form.dob" id="dob" required />
        </div>
  
        <div>
          <label for="gender">Gender:</label>
          <select v-model="form.gender" id="gender" required>
            <option value="" disabled>Select Gender</option>
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="other">Other</option>
          </select>
        </div>
  
        <div>
          <label for="phoneNumber">Phone Number:</label>
          <input type="tel" v-model="form.phoneNumber" id="phoneNumber" required />
        </div>
  
        <!-- Home Address -->
        <h3>Home Address</h3>
        <div>
          <label for="street">Street:</label>
          <input type="text" v-model="form.street" id="street" required />
        </div>
  
        <div>
          <label for="junction">Junction:</label>
          <input type="text" v-model="form.junction" id="junction" required />
        </div>
  
        <div>
          <label for="town">Town:</label>
          <input type="text" v-model="form.town" id="town" required />
        </div>
  
        <!-- Health Information -->
        <h3>Health Information</h3>
        <div>
          <label for="primaryHealthConcern">Primary Health Concern:</label>
          <select v-model="form.primaryHealthConcern" id="primaryHealthConcern" required>
            <option value="" disabled>Select Primary Health Concern</option>
            <option value="woundCare">Wound Care</option>
            <option value="medicationAdministration">Medication Administration</option>
            <option value="healthCheckup">Health Checkup</option>
          </select>
        </div>
  
        <div>
          <label for="medicalHistory">Medical History:</label>
          <textarea v-model="form.medicalHistory" id="medicalHistory" placeholder="List existing conditions" required></textarea>
        </div>
  
        <div>
          <label for="allergies">Known Allergies:</label>
          <textarea v-model="form.allergies" id="allergies" placeholder="Specify any known allergies" required></textarea>
        </div>
  
        <div>
          <label for="medications">Current Medications:</label>
          <textarea v-model="form.medications" id="medications" placeholder="List current medications" required></textarea>
        </div>
  
        <div>
          <label for="recentSurgeries">Recent Surgeries/Procedures:</label>
          <textarea v-model="form.recentSurgeries" id="recentSurgeries" placeholder="Provide details of recent surgeries" required></textarea>
        </div>
  
        <div>
          <label for="recentSymptoms">Recent Symptoms:</label>
          <textarea v-model="form.recentSymptoms" id="recentSymptoms" placeholder="Describe any recent symptoms" required></textarea>
        </div>
  
        <!-- Appointment Details -->
        <h3>Appointment Details</h3>
        <div>
          <label for="appointmentDate">Preferred Appointment Date and Time:</label>
          <input type="datetime-local" v-model="form.appointmentDate" id="appointmentDate" required />
        </div>
  
        <div>
          <label for="nurseGender">Preferred Nurse Gender:</label>
          <select v-model="form.nurseGender" id="nurseGender">
            <option value="" disabled>Select Preference</option>
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="noPreference">No Preference</option>
          </select>
        </div>
  
        <div>
          <label for="specialRequirements">Special Requirements:</label>
          <textarea v-model="form.specialRequirements" id="specialRequirements" placeholder="E.g., language preference, accessibility needs"></textarea>
        </div>
  
        <!-- Consent and Agreements -->
        <h3>Consent and Agreements</h3>
        <div>
          <label for="consentToTreatment">Consent to Treatment:</label>
          <select v-model="form.consentToTreatment" id="consentToTreatment" required>
            <option value="" disabled>Select Yes or No</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>
  
        <div>
          <label for="privacyPolicyAgreement">Privacy Policy Agreement:</label>
          <select v-model="form.privacyPolicyAgreement" id="privacyPolicyAgreement" required>
            <option value="" disabled>Select Yes or No</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>
  
        <div>
          <label for="termsOfServiceAgreement">Terms of Service Agreement:</label>
          <select v-model="form.termsOfServiceAgreement" id="termsOfServiceAgreement" required>
            <option value="" disabled>Select Yes or No</option>
            <option value="yes">Yes</option>
            <option value="no">No</option>
          </select>
        </div>
  
        <div>
          <label for="electronicSignature">Electronic Signature:</label>
          <input type="text" v-model="form.electronicSignature" id="electronicSignature" required />
        </div>
  
        <button type="submit">Submit via WhatsApp</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        form: {
          firstName: '',
          lastName: '',
          dob: '',
          gender: '',
          phoneNumber: '',
          street: '',
          junction: '',
          town: '',
          primaryHealthConcern: '',
          medicalHistory: '',
          allergies: '',
          medications: '',
          recentSurgeries: '',
          recentSymptoms: '',
          appointmentDate: '',
          nurseGender: '',
          specialRequirements: '',
          consentToTreatment: '',
          privacyPolicyAgreement: '',
          termsOfServiceAgreement: '',
          electronicSignature: '',
        },
      };
    },
    methods: {
      submitForm() {
        const message = `Personal Information:
          - First Name: ${this.form.firstName}
          - Last Name: ${this.form.lastName}
          - Date of Birth: ${this.form.dob}
          - Gender: ${this.form.gender}
          - Phone Number: ${this.form.phoneNumber}
  
          Home Address:
          - Street: ${this.form.street}
          - Junction: ${this.form.junction}
          - Town: ${this.form.town}
  
          Health Information:
          - Primary Health Concern: ${this.form.primaryHealthConcern}
          - Medical History: ${this.form.medicalHistory}
          - Allergies: ${this.form.allergies}
          - Medications: ${this.form.medications}
          - Recent Surgeries/Procedures: ${this.form.recentSurgeries}
          - Recent Symptoms: ${this.form.recentSymptoms}
  
          Appointment Details:
          - Preferred Appointment Date and Time: ${this.form.appointmentDate}
          - Preferred Nurse Gender: ${this.form.nurseGender}
          - Special Requirements: ${this.form.specialRequirements}
  
          Consent and Agreements:
          - Consent to Treatment: ${this.form.consentToTreatment}
          - Privacy Policy Agreement: ${this.form.privacyPolicyAgreement}
          - Terms of Service Agreement: ${this.form.termsOfServiceAgreement}
          - Electronic Signature: ${this.form.electronicSignature}
        `;
  
        const encodedMessage = encodeURIComponent(message.trim());
        const phoneNumber = "23772245246";
        const whatsappURL = `https://wa.me/${phoneNumber}?text=${encodedMessage}`;
        
        window.open(whatsappURL, "_blank");
      },
    },
  };
  </script>
  
  <style scoped>
  form div {
    margin-bottom: 15px;
  }
  
  h3 {
    margin-top: 20px;
    color: #42b983;
  }
  
  label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
  }
  
  input, select, textarea {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
  }
  
  button {
    padding: 10px 20px;
    background-color: #42b983;
    color: white;
    border: none;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #359a6e;
  }
  </style>
  