# Ex06 BMI Calculator
## Date: 29.05.2026

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
## DEVELOPED BY: HARINI S
###
```
import { useState } from "react";
import "./BMI.css";

function getCategory(bmi) {
  if (bmi < 18.5) return { cat: "Underweight", color: "#d0e8ff" };
  if (bmi < 25)   return { cat: "Normal weight", color: "#d4edda" };
  if (bmi < 30)   return { cat: "Overweight",    color: "#fff3cd" };
  return           { cat: "Obese",               color: "#f8d7da" };
}

export default function BMI() {
  const [height, setHeight] = useState("");
  const [weight, setWeight] = useState("");
  const [bmi, setBmi]       = useState(null);
  const [error, setError]   = useState("");

  const calculate = () => {
    const h = parseFloat(height);
    const w = parseFloat(weight);
    if (!h || !w || h <= 0 || w <= 0) {
      setError("Please enter valid height and weight."); return;
    }
    setError("");
    const hm = h / 100;
    setBmi((w / (hm * hm)).toFixed(1));
  };

  const reset = () => { setHeight(""); setWeight(""); setBmi(null); setError(""); };

  const result = bmi ? getCategory(parseFloat(bmi)) : null;

  return (
    <div className="container">
      <h2>BMI Calculator</h2>

      {!bmi ? (
        <div className="form">
          <label>Height (cm)</label>
          <input type="number" value={height} onChange={e => setHeight(e.target.value)} placeholder="e.g. 170" />
          <label>Weight (kg)</label>
          <input type="number" value={weight} onChange={e => setWeight(e.target.value)} placeholder="e.g. 65" />
          {error && <p className="error">{error}</p>}
          <button onClick={calculate}>Calculate BMI</button>
        </div>
      ) : (
        <div className="result" style={{ background: result.color }}>
          <h3>Your BMI: {bmi}</h3>
          <p>{result.cat}</p>
          <button onClick={reset}>Calculate Again</button>
        </div>
      )}
    </div>
  );
}
```
### src/BMI.css
```
body { background: #f0f2f5; margin: 0; }

.container {
  max-width: 340px;
  margin: 60px auto;
  background: #fff;
  padding: 2rem;
  border-radius: 10px;
  border: 1px solid #ddd;
  text-align: center;
}

h2 { margin: 0 0 1.5rem; }

.form label { display: block; text-align: left; font-size: 14px; margin-bottom: 4px; color: #555; }

.form input {
  width: 100%; box-sizing: border-box;
  padding: 8px; margin-bottom: 1rem;
  border: 1px solid #ccc; border-radius: 6px; font-size: 14px;
}

.form button, .result button {
  width: 100%; padding: 10px;
  background: #185FA5; color: #fff;
  border: none; border-radius: 6px;
  font-size: 15px; cursor: pointer;
}

.result { padding: 1.5rem; border-radius: 8px; }
.result h3 { font-size: 28px; margin: 0 0 8px; }
.result p  { font-size: 16px; margin: 0 0 1rem; }
.result button { background: #444; }

.error { color: red; font-size: 13px; margin-bottom: 8px; }
```
### App.js
```
import BMI from "./BMI";
export default function App() { return <BMI />; }
```



## OUTPUT

<img width="892" height="361" alt="image" src="https://github.com/user-attachments/assets/720b0dba-9cde-49a6-a8f5-b5b199642540" />

<img width="874" height="395" alt="image" src="https://github.com/user-attachments/assets/a408a507-f191-472a-90fc-f381e3aac90d" />

<img width="855" height="423" alt="image" src="https://github.com/user-attachments/assets/91bcc063-4f3d-4e73-8c39-62943a6f164a" />



## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
