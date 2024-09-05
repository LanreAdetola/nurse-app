<template>
  <div class="form-container">
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
          <option value="other">Other</option> 
        </select>
        <div v-if="form.primaryHealthConcern === 'other'">
          <label for="otherConcern">Please specify:</label>
          <input type="text" v-model="form.otherPrimaryHealthConcern" id="otherConcern" />
        </div>
      </div>

      <div>
        <label for="medicalHistory">Medical History:</label>
        <textarea 
          v-model="form.medicalHistory" 
          id="medicalHistory" 
          placeholder="List existing conditions" 
          :disabled="form.isMedicalHistoryNil" 
          required
        ></textarea>
        <input 
          type="checkbox" 
          v-model="form.isMedicalHistoryNil" 
          id="medicalHistoryNil" 
        />
        <label for="medicalHistoryNil">No Medical History</label>
      </div>

      <div>
        <label for="allergies">Known Allergies:</label>
        <textarea 
          v-model="form.allergies" 
          id="allergies" 
          placeholder="Specify any known allergies" 
          :disabled="form.isAllergiesNil" 
          required
        ></textarea>
        <input 
          type="checkbox" 
          v-model="form.isAllergiesNil" 
          id="allergiesNil" 
        />
        <label for="allergiesNil">No Known Allergies</label>
      </div>

      <div>
        <label for="medications">Current Medications:</label>
        <textarea 
          v-model="form.medications" 
          id="medications" 
          placeholder="List current medications" 
          :disabled="form.isMedicationsNil" 
          required
        ></textarea>
        <input 
          type="checkbox" 
          v-model="form.isMedicationsNil" 
          id="medicationsNil" 
        />
        <label for="medicationsNil">No Current Medications</label>
      </div>

      <div>
        <label for="recentSurgeries">Recent Surgeries/Procedures:</label>
        <textarea 
          v-model="form.recentSurgeries" 
          id="recentSurgeries" 
          placeholder="Provide details of recent surgeries" 
          :disabled="form.isRecentSurgeriesNil" 
          required
        ></textarea>
        <input 
          type="checkbox" 
          v-model="form.isRecentSurgeriesNil" 
          id="recentSurgeriesNil" 
        />
        <label for="recentSurgeriesNil">No Recent Surgeries/Procedures</label>
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

      <button type="submit">Submit via WhatsApp</button>
    </form>
  </div>
</template>

<script>
import jsPDF from 'jspdf';

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
        otherPrimaryHealthConcern: '',
        medicalHistory: '',
        isMedicalHistoryNil: false,
        allergies: '',
        isAllergiesNil: false,
        medications: '',
        isMedicationsNil: false,
        recentSurgeries: '',
        isRecentSurgeriesNil: false,
        recentSymptoms: '',
        appointmentDate: '',
        specialRequirements: '',
        consentToTreatment: '',
        privacyPolicyAgreement: '',
        termsOfServiceAgreement: '',
      },
    };
  },
  methods: {
    submitForm() {
      const doc = new jsPDF();

      // Add title
      doc.setFontSize(18);
      doc.text('Form Details', 14, 20);

      // Add form data
      doc.setFontSize(12);
      let yOffset = 30; // Starting y-offset for the content
      doc.text('Personal Information:', 14, yOffset);
      yOffset += 10;
      doc.text(`First Name: ${this.form.firstName}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Last Name: ${this.form.lastName}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Date of Birth: ${this.form.dob}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Gender: ${this.form.gender}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Phone Number: ${this.form.phoneNumber}`, 14, yOffset);

      yOffset += 20;
      doc.text('Home Address:', 14, yOffset);
      yOffset += 10;
      doc.text(`Street: ${this.form.street}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Junction: ${this.form.junction}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Town: ${this.form.town}`, 14, yOffset);

      yOffset += 20;
      doc.text('Health Information:', 14, yOffset);
      yOffset += 10;
      doc.text(`Primary Health Concern: ${this.form.primaryHealthConcern}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Medical History: ${this.form.medicalHistory}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Allergies: ${this.form.allergies}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Medications: ${this.form.medications}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Recent Surgeries/Procedures: ${this.form.recentSurgeries}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Recent Symptoms: ${this.form.recentSymptoms}`, 14, yOffset);

      yOffset += 20;
      doc.text('Appointment Details:', 14, yOffset);
      yOffset += 10;
      doc.text(`Preferred Appointment Date and Time: ${this.form.appointmentDate}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Special Requirements: ${this.form.specialRequirements}`, 14, yOffset);

      yOffset += 20;
      doc.text('Consent and Agreements:', 14, yOffset);
      yOffset += 10;
      doc.text(`Consent to Treatment: ${this.form.consentToTreatment}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Privacy Policy Agreement: ${this.form.privacyPolicyAgreement}`, 14, yOffset);
      yOffset += 10;
      doc.text(`Terms of Service Agreement: ${this.form.termsOfServiceAgreement}`, 14, yOffset);

      // Save the PDF
      const pdfBlob = doc.output('blob');
      const pdfUrl = URL.createObjectURL(pdfBlob);

      // Open the PDF in a new tab for user download
      window.open(pdfUrl, "_blank");
      
      // Prepare WhatsApp message
      const phoneNumber = "23772245246";
      const whatsappURL = `https://wa.me/${phoneNumber}?text=${encodeURIComponent("Please find the attached form. Unfortunately, direct file sending is not supported. Please download and send manually.")}`;

      // Open WhatsApp in a new tab
      window.open(whatsappURL, "_blank");
    },
  },
};
</script>

<style scoped>
.form-container {
  padding: 1rem;
  margin: 0 auto;
  max-width: 600px; /* Set a max-width for better alignment on large screens */
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem; /* Add space between elements */
}

input, select, textarea {
  padding: 0.75rem; /* Increased padding for better touch interactions */
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 100%; /* Full-width inputs */
  box-sizing: border-box; /* Ensure padding and border are included in the element's total width */
}

button {
  padding: 0.75rem;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  text-align: center;
}

button:hover {
  background-color: #45a049;
}

/* Mobile Optimization */
@media only screen and (max-width: 600px) {
  .form-container {
    padding: 0.5rem;
  }

  input, select, textarea {
    font-size: 1rem;
  }

  button {
    padding: 1rem;
    font-size: 1.1rem;
  }

  h3 {
    font-size: 1.2rem;
  }
}
</style>
