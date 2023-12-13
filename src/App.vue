<template>
  <div class="container">
    <h1 class="work-experience-app">Work Experience App</h1>
    <div class="form">
      <!-- input fields for the numbers -->
      <input type="number" v-model="number1" placeholder="Enter number 1" class="input-field" />
      <input type="number" v-model="number2" placeholder="Enter number 2" class="input-field" />
      <button @click="sendNumbers" class="submit-button">Send Numbers</button>
      <p v-if="confirmationMessage" class="confirmation-message">{{ confirmationMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number1: null,
      number2: null,
      confirmationMessage: ""
    };
  },
  methods: {
    sendNumbers() {
      // send numbers to the API
      fetch("http://127.0.0.1:5000/math", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          number1: this.number1,
          number2: this.number2
        })
      })
      //display the response from the API
        .then(response => response.json())
        .then(data => {
          this.confirmationMessage = "Numbers sent successfully! The API responded with the number: " + data.result;
        })
        .catch(error => {
          console.error("Error:", error);
        });
    }
  }
};
</script>

<style scoped>
.container {
  min-height: 98vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #121212;
}

.form {
  text-align: center;
}
.work-experience-app {
  text-align: center;
  color: white;
  position: absolute;
  top: 35%;
  font-size: 50px;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
.input-field {
  background-color: transparent;
  border: 2px solid #fff;
  border-radius: 5px;
  color: #fff;
  margin: 10px;
  padding: 10px;
  transition: all 0.3s ease;
}

.input-field:focus {
  outline: none;
  border-color: #9b59b6;
  box-shadow: 0 0 10px #9b59b6;
}

.submit-button {
  background-color: transparent;
  border: 2px solid #fff;
  border-radius: 5px;
  color: #fff;
  cursor: pointer;
  padding: 10px 20px;
  transition: all 0.3s ease;
  margin-top: 10px;
}

.submit-button:hover {
  background-color: #9b59b6;
  border-color: #9b59b6;
  box-shadow: 0 0 20px #9b59b6;
}

.confirmation-message {
  color: #fff;
  margin-top: 20px;
}
</style>
