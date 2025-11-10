# bmi.calculator
Simple BMI calculator app
<!DOCTYPE html>
<html lang="sl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>BMI Kalkulator</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
            -webkit-text-size-adjust: 100%;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #333;
            line-height: 1.4;
            padding: 10px;
            min-height: 100vh;
            font-size: 14px;
        }
        
        .container {
            max-width: 100%;
            background: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            overflow: hidden;
            margin: 0 auto;
        }
        
        header {
            background: #4a6fa5;
            color: white;
            padding: 15px 10px;
            text-align: center;
        }
        
        h1 {
            font-size: 1.4rem;
            margin-bottom: 5px;
        }
        
        .subtitle {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        
        .content {
            display: flex;
            flex-direction: column;
            padding: 10px;
        }
        
        .input-section, .results-section {
            width: 100%;
            padding: 10px;
        }
        
        .results-section {
            background: #f8f9fa;
            border-radius: 8px;
            margin-top: 10px;
        }
        
        .form-group {
            margin-bottom: 12px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            font-size: 0.9rem;
        }
        
        input, select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 14px;
            background: white;
        }
        
        button {
            background: #4a6fa5;
            color: white;
            border: none;
            padding: 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            width: 100%;
            margin-top: 5px;
        }
        
        .bmi-result {
            text-align: center;
            padding: 15px;
            margin: 10px 0;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .bmi-value {
            font-size: 2rem;
            font-weight: 700;
            margin: 5px 0;
        }
        
        .bmi-category {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 8px;
        }
        
        .bmi-scale {
            height: 15px;
            background: linear-gradient(to right, #dc3545, #ffc107, #28a745, #ffc107, #dc3545);
            border-radius: 8px;
            margin: 15px 0;
            position: relative;
        }
        
        .bmi-marker {
            position: absolute;
            top: -3px;
            width: 8px;
            height: 21px;
            background: #333;
            border-radius: 4px;
            transform: translateX(-50%);
        }
        
        .details {
            margin-top: 15px;
        }
        
        .detail-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
            font-size: 0.9rem;
        }
        
        .recommendations {
            margin-top: 15px;
            padding: 12px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .recommendations h3 {
            margin-bottom: 8px;
            color: #4a6fa5;
            font-size: 1rem;
        }
        
        .gender-selector {
            display: flex;
            gap: 8px;
        }
        
        .gender-option {
            flex: 1;
            text-align: center;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.9rem;
        }
        
        .gender-option.selected {
            border-color: #4a6fa5;
            background: rgba(74, 111, 165, 0.1);
        }
        
        .underweight { color: #dc3545; }
        .normal { color: #28a745; }
        .overweight { color: #ffc107; }
        .obese { color: #dc3545; }
        
        footer {
            text-align: center;
            padding: 10px;
            margin-top: 10px;
            color: #666;
            font-size: 0.8rem;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>BMI Kalkulator</h1>
            <p class="subtitle">Za mobilno napravo</p>
        </header>
        
        <div class="content">
            <section class="input-section">
                <div class="form-group">
                    <label>Spol</label>
                    <div class="gender-selector">
                        <div class="gender-option" id="male">Moški</div>
                        <div class="gender-option selected" id="female">Ženska</div>
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="age">Starost</label>
                    <input type="number" id="age" min="2" max="120" value="30">
                </div>
                
                <div class="form-group">
                    <label for="height">Višina (cm)</label>
                    <input type="number" id="height" min="50" max="250" value="170">
                </div>
                
                <div class="form-group">
                    <label for="weight">Teža (kg)</label>
                    <input type="number" id="weight" min="10" max="300" value="70">
                </div>
                
                <div class="form-group">
                    <label for="activity">Aktivnost</label>
                    <select id="activity">
                        <option value="1.2">Sedeči</option>
                        <option value="1.375">Rahlo aktiven</option>
                        <option value="1.55">Zmerno aktiven</option>
                        <option value="1.725">Zelo aktiven</option>
                        <option value="1.9">Ekstremno aktiven</option>
                    </select>
                </div>
                
                <button id="calculate">IZRAČUNAJ BMI</button>
            </section>
            
            <section class="results-section">
                <div class="bmi-result">
                    <h2>Vaš BMI</h2>
                    <div class="bmi-value" id="bmiValue">-</div>
                    <div class="bmi-category" id="bmiCategory">-</div>
                    
                    <div class="bmi-scale">
                        <div class="bmi-marker" id="bmiMarker"></div>
                    </div>
                    
                    <div style="display: flex; justify-content: space-between; font-size: 0.8rem;">
                        <span>16</span>
                        <span>18.5</span>
                        <span>25</span>
                        <span>30</span>
                        <span>40</span>
                    </div>
                </div>
                
                <div class="details">
                    <h3>Podrobnosti</h3>
                    <div class="detail-item">
                        <span>Normalno območje:</span>
                        <span>18.5 - 24.9</span>
                    </div>
                    <div class="detail-item">
                        <span>Idealna teža:</span>
                        <span id="idealWeight">-</span>
                    </div>
                    <div class="detail-item">
                        <span>Kalorije na dan:</span>
                        <span id="calories">-</span>
                    </div>
                    <div class="detail-item">
                        <span>Telesna maščoba:</span>
                        <span id="bodyFat">-</span>
                    </div>
                </div>
                
                <div class="recommendations">
                    <h3>Priporočila</h3>
                    <p id="recommendationsText">Vnesite podatke za priporočila.</p>
                </div>
            </section>
        </div>
        
        <footer>
            <p>Za informativne namene</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const genderOptions = document.querySelectorAll('.gender-option');
            const calculateButton = document.getElementById('calculate');
            const bmiValue = document.getElementById('bmiValue');
            const bmiCategory = document.getElementById('bmiCategory');
            const bmiMarker = document.getElementById('bmiMarker');
            const idealWeight = document.getElementById('idealWeight');
            const calories = document.getElementById('calories');
            const bodyFat = document.getElementById('bodyFat');
            const recommendationsText = document.getElementById('recommendationsText');
            
            let selectedGender = 'female';
            
            // Izbor spola
            genderOptions.forEach(option => {
                option.addEventListener('click', function() {
                    genderOptions.forEach(opt => opt.classList.remove('selected'));
                    this.classList.add('selected');
                    selectedGender = this.id;
                });
            });
            
            // Izračun BMI
            calculateButton.addEventListener('click', function() {
                const age = parseInt(document.getElementById('age').value);
                const height = parseInt(document.getElementById('height').value);
                const weight = parseInt(document.getElementById('weight').value);
                const activity = parseFloat(document.getElementById('activity').value);
                
                if (!age || !height || !weight) {
                    alert('Vnesite vse podatke!');
                    return;
                }
                
                // Izračun BMI
                const heightInMeters = height / 100;
                const bmi = weight / (heightInMeters * heightInMeters);
                const roundedBmi = bmi.toFixed(1);
                
                // Določitev kategorije BMI
                let category, categoryClass;
                if (bmi < 16) {
                    category = 'Huda podhranjenost';
                    categoryClass = 'underweight';
                } else if (bmi >= 16 && bmi < 17) {
                    category = 'Zmerna podhranjenost';
                    categoryClass = 'underweight';
                } else if (bmi >= 17 && bmi < 18.5) {
                    category = 'Blaga podhranjenost';
                    categoryClass = 'underweight';
                } else if (bmi >= 18.5 && bmi < 25) {
                    category = 'Normalna teža';
                    categoryClass = 'normal';
                } else if (bmi >= 25 && bmi < 30) {
                    category = 'Prekomerna teža';
                    categoryClass = 'overweight';
                } else if (bmi >= 30 && bmi < 35) {
                    category = 'Debelost 1. stopnje';
                    categoryClass = 'obese';
                } else if (bmi >= 35 && bmi < 40) {
                    category = 'Debelost 2. stopnje';
                    categoryClass = 'obese';
                } else {
                    category = 'Debelost 3. stopnje';
                    categoryClass = 'obese';
                }
                
                // Prikaz rezultatov
                bmiValue.textContent = roundedBmi;
                bmiCategory.textContent = category;
                bmiCategory.className = 'bmi-category ' + categoryClass;
                
                // Premikanje markerja
                let markerPosition = ((bmi - 16) / (40 - 16)) * 100;
                if (markerPosition < 0) markerPosition = 0;
                if (markerPosition > 100) markerPosition = 100;
                bmiMarker.style.left = markerPosition + '%';
                
                // Idealna teža
                let idealWeightValue;
                if (selectedGender === 'male') {
                    idealWeightValue = 50 + 0.9 * (height - 152);
                } else {
                    idealWeightValue = 45.5 + 0.9 * (height - 152);
                }
                idealWeight.textContent = idealWeightValue.toFixed(1) + ' kg';
                
                // Kalorije
                let bmr;
                if (selectedGender === 'male') {
                    bmr = 10 * weight + 6.25 * height - 5 * age + 5;
                } else {
                    bmr = 10 * weight + 6.25 * height - 5 * age - 161;
                }
                const dailyCalories = Math.round(bmr * activity);
                calories.textContent = dailyCalories + ' kcal';
                
                // Telesna maščoba
                let bodyFatPercentage;
                if (selectedGender === 'male') {
                    bodyFatPercentage = (1.20 * bmi) + (0.23 * age) - 16.2;
                } else {
                    bodyFatPercentage = (1.20 * bmi) + (0.23 * age) - 5.4;
                }
                bodyFat.textContent = bodyFatPercentage.toFixed(1) + '%';
                
                // Priporočila
                let recommendations = '';
                if (bmi < 18.5) {
                    recommendations = 'Vaš BMI kaže na podhranjenost. Priporočamo povečanje vnosa hranil. Posvetujte se s strokovnjakom.';
                } else if (bmi >= 18.5 && bmi < 25) {
                    recommendations = 'Čestitamo! Vaš BMI je v normalnem območju. Ohranjajte zdrave navade.';
                } else if (bmi >= 25 && bmi < 30) {
                    recommendations = 'Vaš BMI kaže na prekomerno težo. Priporočamo zmerno zmanjšanje kalorij in več gibanja.';
                } else {
                    recommendations = 'Vaš BMI kaže na debelost. Priporočamo posvet z zdravnikom za varno izgubo teže.';
                }
                
                recommendationsText.textContent = recommendations;
            });
            
            // Samodejni izračun ob nalaganju
            calculateButton.click();
        });
    </script>
</body>
</html>
