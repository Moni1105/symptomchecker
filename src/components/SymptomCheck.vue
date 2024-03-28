<template>
<div>
  <p><label for="symptoms">Enter your symptoms:</label></p>
    <textarea v-model="userSymptoms" id="symptoms" name="symptoms" rows="10" cols="50"></textarea>
    <p>(eg: I have red eyes for the last 3 days)</p>
    <div class="button-container">
    <button class="button-1" @click="fetchData">Check Results</button> 
    
    <button class="button-1" @click="clearFields">Clear</button>
    </div>
    <div class="output-container">
      <h2>Symptom Checker Results</h2>
       <div class="section">
        <h3 v-if="potentialCauses.length > 0" >Possible Diagnosis</h3>
        <ul v-for="cause in potentialCauses" :key="cause">{{ cause }}
        </ul>
      </div>
      <div class="section">
        <h3 v-if="followupQuestions.length > 0">Questions?</h3>
        <ul v-for="question in followupQuestions" :key="question">{{ question }}
          
        </ul>
      </div>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
name:'SymptomCheck',
data() {
    return {
      userSymptoms: '',
      potentialCauses: [],
      followupQuestions: []
    };
  },
  methods: {
    async fetchData() {
      if(!this.userSymptoms){
        return alert("Please enter symptoms");
      }
      try {
        const response = await axios.post('https://symptom-checker4.p.rapidapi.com/analyze', {
          symptoms: this.userSymptoms
        }, {
          headers: {
            'content-type': 'application/json',
            'X-RapidAPI-Key': process.env.VUE_APP_API_KEY,
            'X-RapidAPI-Host': 'symptom-checker4.p.rapidapi.com'
          }
        });
        console.log(response);
        this.potentialCauses = response.data.potentialCauses;
        console.log(this.potentialCauses)
        this.followupQuestions = response.data.followupQuestions;
        console.log(this.followupQuestions)
      } catch (error) {
        console.error(error);
      }
    },
    clearFields() {
      this.userSymptoms = '';
      this.potentialCauses = [];
      this.followupQuestions = [];
    }
  }
};

</script>

<style>
body {
    background-color: #8EC5FC;
    background-image: linear-gradient(62deg, #8EC5FC 0%, #E0C3FC 100%);
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

.output-container {
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: fit-content;
    margin: 0 auto;
    /* Center the output container horizontally */
    margin-top: 20px;
    /* Adjust top margin as needed */
}

h2 {
    color: #333;
}
.button-container {
  display: flex;
  justify-content: center; /* Align buttons horizontally */
  gap: 10px; /* Space between buttons */
}

.section {
    margin-bottom: 20px;
}

.section h3 {
    margin-bottom: 10px;
}

.section ul {
    list-style-type: none;
    padding-left: 0;
}

.section ul li {
    margin-bottom: 5px;
}

#output {
    color: black;
    /* Set text color to black for better readability */
}


/* CSS */
.button-1 {
    background-color: #4e2575;
    border-radius: 8px;
    border-style: none;
    box-sizing: border-box;
    color: #FFFFFF;
    cursor: pointer;
    display: inline-block;
    font-family: "Haas Grot Text R Web", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 14px;
    font-weight: 500;
    height: 40px;
    line-height: 20px;
    list-style: none;
    margin: 0;
    outline: none;
    padding: 10px 16px;
    position: relative;
    text-align: center;
    text-decoration: none;
    transition: color 100ms;
    vertical-align: baseline;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
}

.button-1:hover,
.button-1:focus {
    background-color: #4e2575;
}
</style>