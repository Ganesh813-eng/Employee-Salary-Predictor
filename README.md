# Employee-Salary-Predictor

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Employee Salary Prediction</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
      rel="stylesheet"
    />
    <link
      href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap"
      rel="stylesheet"
    />
    <style>
      body {
        font-family: 'Inter', sans-serif;
      }
    </style>
  </head>
  <body class="bg-gray-50 min-h-screen flex flex-col">
    <header class="bg-white shadow">
      <div class="container mx-auto px-4 py-5 flex items-center justify-between">
        <div class="flex items-center space-x-3">
          <img
            src="https://storage.googleapis.com/a1aa/image/8d826aab-f338-404e-e9a1-a8314662b91a.jpg"
            alt="Company logo with stylized letters E and S in blue and gray"
            class="w-10 h-10"
            width="40"
            height="40"
          />
          <h1 class="text-2xl font-semibold text-gray-800">Employee Salary Predictor</h1>
        </div>
        <nav class="hidden md:flex space-x-6 text-gray-600 font-medium">
          <a href="#" class="hover:text-blue-600 transition">Home</a>
          <a href="#" class="hover:text-blue-600 transition">About</a>
          <a href="#" class="hover:text-blue-600 transition">Contact</a>
        </nav>
        <button
          id="menu-btn"
          aria-label="Toggle menu"
          class="md:hidden text-gray-600 focus:outline-none focus:ring-2 focus:ring-blue-600"
        >
          <i class="fas fa-bars fa-lg"></i>
        </button>
      </div>
      <nav id="mobile-menu" class="hidden md:hidden bg-white border-t border-gray-200">
        <a href="#" class="block px-4 py-3 text-gray-700 hover:bg-gray-100">Home</a>
        <a href="#" class="block px-4 py-3 text-gray-700 hover:bg-gray-100">About</a>
        <a href="#" class="block px-4 py-3 text-gray-700 hover:bg-gray-100">Contact</a>
      </nav>
    </header>

    <main class="flex-grow container mx-auto px-4 py-10 max-w-3xl">
      <section class="bg-white rounded-lg shadow p-8">
        <h2 class="text-3xl font-semibold text-gray-800 mb-6 text-center">Predict Your Salary</h2>
        <form class="space-y-6" id="salary-form">
          <div>
            <label for="experience" class="block text-gray-700 font-medium mb-2">Years of Experience</label>
            <input
              type="number"
              id="experience"
              name="experience"
              min="0"
              step="0.1"
              placeholder="e.g. 3.5"
              required
              class="w-full border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
          </div>
          <div>
            <label for="education" class="block text-gray-700 font-medium mb-2">Education Level</label>
            <select
              id="education"
              name="education"
              required
              class="w-full border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
              <option value="" disabled selected>Select your education</option>
              <option value="highschool">High School</option>
              <option value="bachelor">Bachelor's Degree</option>
              <option value="master">Master's Degree</option>
              <option value="phd">PhD</option>
            </select>
          </div>
          <div>
            <label for="job-role" class="block text-gray-700 font-medium mb-2">Job Role</label>
            <select
              id="job-role"
              name="job-role"
              required
              class="w-full border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
              <option value="" disabled selected>Select your job role</option>
              <option value="software_engineer">Software Engineer</option>
              <option value="data_scientist">Data Scientist</option>
              <option value="product_manager">Product Manager</option>
              <option value="designer">Designer</option>
              <option value="sales">Sales</option>
              <option value="hr">Human Resources</option>
            </select>
          </div>
          <div>
            <label for="location" class="block text-gray-700 font-medium mb-2">Location</label>
            <select
              id="location"
              name="location"
              required
              class="w-full border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
              <option value="" disabled selected>Select your location</option>
              <option value="new_york">New York, USA</option>
              <option value="san_francisco">San Francisco, USA</option>
              <option value="london">London, UK</option>
              <option value="berlin">Berlin, Germany</option>
              <option value="bangalore">Bangalore, India</option>
              <option value="remote">Remote</option>
            </select>
          </div>
          <button
            type="submit"
            class="w-full bg-blue-600 text-white font-semibold py-3 rounded-md hover:bg-blue-700 transition"
          >
            Predict Salary
          </button>
        </form>
        <div
          id="result"
          role="alert"
          aria-live="polite"
          class="mt-8 p-6 bg-blue-50 border border-blue-300 rounded-md text-center text-blue-800 text-xl font-semibold hidden"
        ></div>
      </section>
    </main>

    <footer class="bg-white border-t border-gray-200 py-6 mt-12">
      <div class="container mx-auto px-4 text-center text-gray-600 text-sm">
        © 2024 Employee Salary Predictor. All rights reserved.
      </div>
    </footer>

    <script>
      const menuBtn = document.getElementById('menu-btn');
      const mobileMenu = document.getElementById('mobile-menu');

      menuBtn.addEventListener('click', () => {
        mobileMenu.classList.toggle('hidden');
      });

      const form = document.getElementById('salary-form');
      const resultDiv = document.getElementById('result');

      function predictSalary({ experience, education, jobRole, location }) {
        let base = 30000;
        base += experience * 2500;

        switch (education) {
          case 'highschool': base += 0; break;
          case 'bachelor': base += 10000; break;
          case 'master': base += 20000; break;
          case 'phd': base += 30000; break;
        }

        switch (jobRole) {
          case 'software_engineer': base += 20000; break;
          case 'data_scientist': base += 25000; break;
          case 'product_manager': base += 22000; break;
          case 'designer': base += 15000; break;
          case 'sales': base += 12000; break;
          case 'hr': base += 10000; break;
        }

        switch (location) {
          case 'new_york': base *= 1.3; break;
          case 'san_francisco': base *= 1.4; break;
          case 'london': base *= 1.2; break;
          case 'berlin': base *= 1.1; break;
          case 'bangalore': base *= 0.7; break;
          case 'remote': base *= 1.0; break;
        }

        return Math.round(base);
      }

      form.addEventListener('submit', (e) => {
        e.preventDefault();
        const experience = parseFloat(form.experience.value);
        const education = form.education.value;
        const jobRole = form['job-role'].value;
        const location = form.location.value;

        if (isNaN(experience) || !education || !jobRole || !location || experience < 0) {
          resultDiv.textContent = 'Please fill out all fields correctly.';
          resultDiv.classList.remove('hidden');
          return;
        }

        const salary = predictSalary({ experience, education, jobRole, location });
        resultDiv.textContent = `Estimated Annual Salary: $${salary.toLocaleString()}`;
        resultDiv.classList.remove('hidden');
      });
    </script>
  </body>
</html>
