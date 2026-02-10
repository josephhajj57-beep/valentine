from flask import Flask, render_template_string

app = Flask(__name__)

# Updated colors: White Envelope + Red Heart
html_layout = """
<!DOCTYPE html>
<html>
<head>
    <title>White Valentine Envelope</title>
    <style>
        body {
            background-color: #1a1a2e; /* Dark background to make white pop */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: 'Arial', sans-serif;
        }

        .envelope-wrapper {
            position: relative;
            cursor: pointer;
        }

        /* The Front of the Envelope (White) */
        .envelope {
            position: relative;
            width: 300px;
            height: 200px;
            background-color: #ffffff; /* White */
            border-radius: 0 0 5px 5px;
            z-index: 3; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        /* The Top Flap (White/Light Gray) */
        .envelope-lid {
            position: absolute;
            top: 0;
            left: 0;
            width: 0;
            height: 0;
            border-top: 120px solid #f2f2f2; /* Light gray so you can see the flap shape */
            border-left: 150px solid transparent;
            border-right: 150px solid transparent;
            transform-origin: top;
            transition: all 0.6s ease-in-out;
            z-index: 4;
        }

        /* The Card - Hidden behind the white envelope */
        .card {
            position: absolute;
            bottom: 10px;
            left: 10px;
            width: 280px;
            height: 170px;
            background: #ffffff;
            padding: 20px;
            box-sizing: border-box;
            border-radius: 5px;
            transition: all 0.6s ease-in-out;
            z-index: 2; /* Hidden behind the envelope layer */
            text-align: center;
            border: 1px solid #eee;
        }

        /* Animation Trigger */
        .envelope-wrapper:hover .envelope-lid {
            transform: rotateX(180deg);
            z-index: 1;
        }

        .envelope-wrapper:hover .card {
            transform: translateY(-150px);
            z-index: 5; /* Card pops to the front */
        }

        /* Red Heart Seal */
        .heart-seal {
            position: absolute;
            top: 100px;
            left: 50%;
            width: 30px;
            height: 30px;
            background-color: #ff0000; /* Red Heart */
            transform: translate(-50%, -50%) rotate(45deg);
            z-index: 5;
            transition: opacity 0.3s;
        }
        .heart-seal::before, .heart-seal::after {
            content: "";
            position: absolute;
            width: 30px; height: 30px;
            background-color: #ff0000;
            border-radius: 50%;
        }
        .heart-seal::before { top: -15px; left: 0; }
        .heart-seal::after { left: -15px; top: 0; }

        .envelope-wrapper:hover .heart-seal {
            opacity: 0;
        }
    </style>
</head>
<body>

    <div class="envelope-wrapper">
        <div class="envelope-lid"></div>
        <div class="heart-seal"></div>
        <div class="card">
            <h3 style="color: #ff0000; margin: 0;">To my love,</h3>
            <p style="font-size: 14px; color: #333; margin-top: 15px;">
                From the moment I first saw you, I knew I wanted to smell your farts forever.
            </p>
            <p style="font-weight: bold; color: #ff0000;">Happy Valentine's Day! ❤️</p>
        </div>
        <div class="envelope"></div>
    </div>

</body>
</html>
"""

@app.route('/')
def home():
    return render_template_string(html_layout)

if __name__ == '__main__':
    app.run(debug=True)
