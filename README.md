# Ex.05 Design a Website for Server Side Processing
# Date:11/04/2025
# AIM:
To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side.

# FORMULA:
P = I2R
P --> Power (in watts)
 I --> Intensity
 R --> Resistance

# DESIGN STEPS:
## Step 1:
Clone the repository from GitHub.

## Step 2:
Create Django Admin project.

## Step 3:
Create a New App under the Django Admin project.

## Step 4:
Create python programs for views and urls to perform server side processing.

## Step 5:
Create a HTML file to implement form based input and output.

## Step 6:
Publish the website in the given URL.

# PROGRAM :

math.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Power Calculator</title>
    <style type="text/css">
        body {
            background-color: #bdd1d3;
            background-repeat: no-repeat;
            background-position: center;
            background-size: cover;
            text-align: center;
            font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
            color: #006064;
        }
        h1 {
            font-size: 2.5em;
            margin-bottom: 20px;
        }
        .container {
            background-color: #c9c4b7;
            border-radius: 100%;
            padding: 75px;
            box-shadow: 0 0 10px #f71bdd;
            display: inline-block;
            margin-top: 50px;
        }
        label {
            font-size: 150%;
            display: block;
            margin: 15px 0 5px;
        }
        input[type="text"] {
            width: 75%;
            padding: 10px;
            border-radius: 12px;
            border: 1px solid #051313;
            margin-bottom: 15px;
            font-size: 1em;
        }
        input[type="submit"] {
            background-color: #1fe374;
            color: rgb(211, 241, 247);
            border: none;
            border-radius: 10px;
            padding: 10px 21px;
            font-size: 1em;
            cursor: pointer;
        }
        input[type="submit"]:hover {
            background-color: #d588b2;
        }
        p {
            font-size: 1.2em;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>The Power of the Bulb</h1>
    <div class="container">
        <form method="POST">
            {% csrf_token %}
            <label>Intensity (A):</label>
            <input type="text" name="intensity" value="{{ I }}">

            <label>Resistance (Ohm):</label>
            <input type="text" name="resistance" value="{{ R }}">

            <br><br>
            <input type="submit" value="Calculate">

            <br><br>
            <label>Power (Watts):</label>
            <input type="text" name="power" value="{{ power }}" readonly>
        </form>
    </div>
</body>
</html>

```

Views.py
```
from django.shortcuts import render

def power_calculate(request):
    context = {
        'power': "",
        'I': "",
        'R': ""
    }

    if request.method == 'POST':
        try:
            I = float(request.POST.get('intensity', '0'))
            R = float(request.POST.get('resistance', '0'))

            power = (I ** 2) * R
            context['power'] = f"{power:.2f}"
            context['I'] = I
            context['R'] = R

            print("POST method is used")
            print(f"Intensity (A) = {I}")
            print(f"Resistance (Ohm) = {R}")
            print(f"Power (Watts) = {power}")

        except ValueError:
            context['power'] = "Invalid input"

    return render(request, 'mathapp/math.html', context)

```

urls.py
```
from django.contrib import admin
from django.urls import path
from mathapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('powerofbulb/', views.power_calculate, name="powerofbulb"),
    path('', views.power_calculate, name="home")
]

```
# SERVER SIDE PROCESSING:
![Screenshot 2024-12-07 213530](https://github.com/user-attachments/assets/0805a612-43cc-4c64-b3fd-3e5c48365ab6)

# HOMEPAGE:
![Screenshot 2024-12-07 213559](https://github.com/user-attachments/assets/f4e10396-5b9d-49a1-989f-52497ffdb6c6)

# RESULT:
The program for performing server side processing is completed successfully.
