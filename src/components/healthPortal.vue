<template>
  <div>
    <a class="github-link" href="https://github.com/Moni1105/symptomchecker">
        Please click here to access Github repository link for this implementation
    </a>
    <div class="container">
      <div class="left-container">
        <h2>Select an Option:</h2>
        <button class="button-2" @click="showSymptomChecker">
          Symptom Checker
        </button>

        <button class="button-2" @click="showHealthInformation">
          General Health Information
        </button>

        <!-- Symptom Checker Content -->
        <div v-if="showSymptomCheckerContent">
          <h2>Symptom Checker</h2>
          <p>Please enter your symptoms:</p>
          <textarea v-model="userSymptoms" rows="10" cols="50"></textarea>
          <br />
          <p>(eg 1: I have red eyes for last 3 days)</p>
          <p>
            (eg 2:I am 35 years old female and having severe head ache for last
            5 days)
          </p>
          <button class="button-1" @click="fetchData">Check Results</button>
          <button class="button-1" @click="clearFields">Clear</button>
          <br /><br />
          <div class="output-container">
            <h3>Symptom Checker Results</h3>
            <div class="section">
              <ul>
                <li v-for="cause in potentialCauses" :key="cause">
                  {{ cause }}
                </li>
              </ul>
            </div>
            <div class="section">
              <ul>
                <li v-for="question in followupQuestions" :key="question">
                  {{ question }}
                </li>
              </ul>
            </div>
          </div>
        </div>

        <!-- General Health Information Content -->
        <div v-if="showHealthInformationContent">
          <h2>General Health Information</h2>
          <p>Please provide the following information:</p>
          <label for="gender">Gender:</label>
          <select v-model="gender" name="gender">
            <option value="male">Male</option>
            <option value="female">Female</option></select
          ><br /><br />
          <label for="age">Age:</label>
          <input
            type="number"
            v-model="age"
            name="age"
            min="1"
            max="150"
          /><br /><br />
          <button class="button-1" @click="fetchHealthData">
            Fetch Health Data
          </button>
          <br /><br />
          <div class="output-container">
            <h2>Heath info results</h2>
            <h3>{{ healthheading }}</h3>
            <div id="healthInfoText">
              <p v-for="resource in healthResources" :key="resource.Title">
                <a :href="resource.AccessibleVersion || '#'">{{
                  resource.Title
                }}</a>
              </p>
            </div>
          </div>
        </div>
        <div class="implementation-description">
          <h2>Application Description:</h2>
          <ul>
            <li>
              <b>Application Description:</b> This application provides two
              functional services: Symptom Checker and General Health
              Information, located on the left side of this HTML page.
            </li>
            <li>
              The <b>Symptom Checker</b> functionality aims to diagnose possible
              diseases and situations that may be encountered by a patient based
              on the symptoms provided by the user.
            </li>
            <li>
              The <b>General Health Information</b> functionality provides
              US-based preventive measures, healthcare information, questions to
              ask a doctor, and a list of tests that should be done by a person
              based on the user's gender and age.
            </li>
          </ul>
        </div>
      </div>

      <div class="right-container">
        <!-- Implementation Description -->
        <div class="implementation-description">
          <h2>Implementation Description:</h2>
          <ul>
            <li>
              <b>Strategy:</b> Implementing the integration of external APIs
              within a framework-based frontend application
            </li>
            <li><b>Framework:</b> Vue 3</li>
            <li>
              <b>External APIs used:</b> SymptomChecker (Rapid API) and
              HealthFinder (Gov Free API)
            </li>
            <li><b>API Integration:</b> Axios library functions</li>
            <li>
              <b>Render.com:</b> To host this application on the internet and
              allow anyone to access it
            </li>
            <li>
              <b>Symptom Checker:</b> If you click on symptom checker button on
              left side. It opens the block showing input box for user to enter
              thier symptoms, when user click on "check results" button,
              performs th api(symptom_checker) call and fetch the response to
              user. Clear button will clear output results and user input.
            </li>
            <li>
              <b>General Health Information:</b> If you click on General Health
              Information button on left side. Allows user to enter information
              about gender and age , when user click on "fetch Health data"
              button, performs th api(Health Finder) call and display the
              response to user. Clear button will clear output results and user
              input.
            </li>
          </ul>
        </div>

        <!-- Client-Server Architecture Diagram -->
        <div class="client-server-architecture-diagram">
          <h2>Client-Server Architecture Diagram:</h2>
          <img
            src="@/assets/Vue_client_server_diagram.png"
            alt="Client-Server Architecture Diagram"
            width="500"
            height="400"
          />
        </div>
      </div>
    </div>
    <table>
      <tr>
        <th>Topics</th>
        <th>Project findings</th>
      </tr>
      <tr>
        <td>Ease of Developing</td>
        <td>
          <strong>Pros:</strong> Setting up the Vue framework is
          straightforward, requiring minimal configuration and only a few steps.
          Vue's extensive collection of directives like v-model, v-for, and
          v-if, simplifies frontend development by providing functionalities for
          managing data binding, iteration, and conditional rendering.
          <br /><strong>Cons:</strong> Beginners might find it tricky to
          understand all the cool things Vue can do. As projects get bigger and
          more complicated, it becomes important to plan carefully and keep
          everything organized to avoid problems.
        </td>
      </tr>
      <tr>
        <td>Developer Community Support</td>
        <td>
          I can find lot of youtube tutorials of Vue framework and also support
          from other various sources.
        </td>
      </tr>
      <tr>
        <td>Error Handling and Debugging</td>
        <td>
          Vue helps you find and fix errors in your code easily. It gives clear
          messages when something goes wrong and shows where the error is
          occured. Vue's built-in DevTools extension let you see what's
          happening in your app in real-time, making it faster to figure out and
          solve issues.
        </td>
      </tr>
      <tr>
        <td>API Integration Details</td>
        <td>
          Vue.js can integrate external APIs using Axios, Fetch API, Vue
          Resource, custom methods, or specialized Vue plugins, each offering
          varying levels of ease and functionality for making HTTP requests and
          handling API responses.<br/>
          I have used axios helper library for both APIs by importing them and calling axios.get() and axios.put() method.
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "healthPortal",
  data() {
    return {
      showSymptomCheckerContent: false,
      showHealthInformationContent: false,
      userSymptoms: "",
      gender: "male",
      age: 1,
      potentialCauses: [],
      followupQuestions: [],
      healthheading: "",
      healthInfoText: "",
    };
  },
  methods: {
    showSymptomChecker() {
      this.showSymptomCheckerContent = true;
      this.showHealthInformationContent = false;
    },
    showHealthInformation() {
      this.showSymptomCheckerContent = false;
      this.showHealthInformationContent = true;
    },
    async fetchData() {
      if (!this.userSymptoms) {
        return alert("Please enter symptoms");
      }
      try {
        //console.log(process.env.VUE_APP_API_KEY)
        const response = await axios.post(
          "https://symptom-checker4.p.rapidapi.com/analyze",
          {
            symptoms: this.userSymptoms,
          },
          {
            headers: {
              "content-type": "application/json",
              "X-RapidAPI-Key": process.env.VUE_APP_API_KEY,
              "X-RapidAPI-Host": "symptom-checker4.p.rapidapi.com",
            },
          }
        );
        console.log(response);
        this.potentialCauses = response.data.potentialCauses;
        console.log(this.potentialCauses);
        this.followupQuestions = response.data.followupQuestions;
        console.log(this.followupQuestions);
      } catch (error) {
        console.error(error);
      }
    },
    clearFields() {
      this.userSymptoms = "";
      this.potentialCauses = [];
      this.followupQuestions = [];
    },
    async fetchHealthData() {
      // Validate age input
      if (!this.age || isNaN(this.age) || this.age <= 0) {
        alert("Please enter a valid age.");
        return;
      }

      // Construct the URL with parameters
      const apiUrl =
        "https://health.gov/myhealthfinder/api/v3/myhealthfinder.json";
      const urlWithParams = `${apiUrl}?age=${this.age}&sex=${this.gender}`;

      try {
        // Make GET request using Axios
        const response = await axios.get(urlWithParams);
        const apiResult = response.data;

        // Extract data from API result
        const heading = apiResult.Result.MyHFHeading;
        const resources = apiResult.Result.Resources.all.Resource;

        // Update Vue reactive data properties
        this.healthheading = heading;
        this.healthResources = resources;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style>
body {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
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

.button-2 {
  background-color: #ea4c89;
  border-radius: 8px;
  border-style: none;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: inline-block;
  font-family: "Haas Grot Text R Web", "Helvetica Neue", Helvetica, Arial,
    sans-serif;
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

.button-2:hover,
.button-2:focus {
  background-color: #f082ac;
}

/* CSS */
.button-1 {
  background-color: #4e2575;
  border-radius: 8px;
  border-style: none;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: inline-block;
  font-family: "Haas Grot Text R Web", "Helvetica Neue", Helvetica, Arial,
    sans-serif;
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
.container {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 20px;
}
.left-container {
  width: 48%; /* Adjust as needed */
}
.right-container {
  width: 48%; /* Adjust as needed */
}
label {
  font-weight: bold;
  display: block; /* Ensures labels appear on their own line */
  margin-bottom: 5px; /* Adds some space between labels */
}

/* Style for select element */
select {
  width: 40%; /* Makes the select element full-width */
  padding: 8px; /* Adds padding for better appearance */
  border-radius: 4px; /* Adds rounded corners */
  border: 2px solid #591769; /* Adds a border */
  box-sizing: border-box; /* Ensures padding and border are included in width */
  margin-bottom: 10px; /* Adds some space between elements */
}

/* Style for input element */
textarea {
  padding: 8px; /* Adds padding for better appearance */
  border-radius: 4px; /* Adds rounded corners */
  border: 2px solid #591769; /* Adds a border */
  box-sizing: border-box; /* Ensures padding and border are included in width */
  margin-bottom: 10px; /* Adds some space between elements */
}
input[type="number"] {
  width: 40%; /* Makes the input element full-width */
  padding: 8px; /* Adds padding for better appearance */
  border-radius: 4px; /* Adds rounded corners */
  border: 2px solid #591769; /* Adds a border */
  box-sizing: border-box; /* Ensures padding and border are included in width */
  margin-bottom: 10px; /* Adds some space between elements */
}
.implementation-description ul {
  list-style-type: disc; /* Use disc for bullet points */
  margin-left: 20px; /* Adjust margin for indentation */
}

.implementation-description li {
  margin-bottom: 5px; /* Adjust margin between items */
  text-align: left;
}

table {
  border: 1px solid #591769;
  border-collapse: collapse;
  width: 100%;
}

th,
td {
  border: 1px solid #591769;
  padding: 10px;
}

th {
  background-color: #ea4c89;
  font-weight: bold;
}
 .github-link {
    position: absolute;
    top: 10px;
    right: 10px;
}
</style>
