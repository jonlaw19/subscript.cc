---
layout: default
title: Subscript and Superscript Generator
---

<!-- Subscript and Superscript Generator -->

<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&family=Open+Sans:wght@400;600&display=swap" rel="stylesheet">

<style>
    /* CSS Variables for easy theming */
    :root {
        --primary-color: #6200ea;
        --secondary-color: #03dac6;
        --symbol-color: #008080; /* Modern Teal for symbols */
        --equation-color: #FF5722; /* Vibrant Orange for equations */
        --action-button-border: #cccccc; /* Light Grey Border for action buttons */
        --action-button-shadow: 0 2px 4px rgba(0,0,0,0.1); /* Subtle Drop Shadow */
        --action-button-text: #000000; /* Black Text for action buttons */
        --background-color: #f0f2f5;
        --card-background: #ffffff;
        --text-color: #333333;
        --border-color: #e0e0e0;
        --error-color: #b00020;
        --font-family: 'Roboto', sans-serif;
        --transition-speed: 0.3s;
    }

    /* Dark mode variables */
    body.dark-mode {
        --background-color: #121212;
        --card-background: #1e1e1e;
        --text-color: #ffffff;
        --border-color: #333333;
        --primary-color: #bb86fc;
        --secondary-color: #03dac6;
        --symbol-color: #40e0d0; /* Light Teal for symbols in dark mode */
        --equation-color: #ff8a65; /* Light Orange for equations in dark mode */
        --action-button-border: #555555; /* Darker Grey Border for action buttons in dark mode */
        --action-button-shadow: 0 2px 4px rgba(255,255,255,0.1); /* Light Drop Shadow in dark mode */
        --action-button-text: #ffffff; /* White Text for action buttons in dark mode */
    }

    /* Base styles */
    body {
        font-family: var(--font-family);
        margin: 0;
        padding: 20px;
        background-color: var(--background-color);
        color: var(--text-color);
        transition: background-color var(--transition-speed), color var(--transition-speed);
    }

    h1 {
        text-align: center;
        margin-bottom: 30px;
        font-weight: 700;
        color: var(--primary-color);
    }

    label {
        font-weight: 500;
        display: block;
        margin-bottom: 8px;
    }

    .container {
        max-width: 1200px;
        margin: 0 auto;
    }

    .input-section, .output-section, .character-bank-section, .equation-bank-section, .options-section, .actions-section {
        background-color: var(--card-background);
        padding: 20px;
        margin-bottom: 20px;
        border-radius: 8px;
        box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        transition: background-color var(--transition-speed), box-shadow var(--transition-speed);
    }

    textarea, input[type="text"], input[type="range"] {
        width: 100%;
        padding: 12px 16px;
        margin: 10px 0 20px;
        font-size: 16px;
        border: 1px solid var(--border-color);
        border-radius: 6px;
        box-sizing: border-box;
        transition: border-color var(--transition-speed);
        font-family: inherit;
    }

    textarea:focus, input[type="text"]:focus {
        border-color: var(--primary-color);
        outline: none;
    }

    /* General Button Styles */
    button {
        padding: 10px 20px;
        font-size: 16px;
        cursor: pointer;
        margin-right: 10px;
        border: none;
        border-radius: 6px;
        background-color: var(--primary-color);
        color: #ffffff;
        transition: background-color var(--transition-speed), transform var(--transition-speed);
        font-family: inherit;
    }

    button:hover {
        background-color: #3700b3; /* Darker shade for hover */
        transform: translateY(-2px);
    }

    button:active {
        transform: translateY(0);
    }

    /* Action Buttons Specific Styles */
    .actions-section button {
        background-color: transparent;
        border: 1px solid var(--action-button-border);
        color: var(--action-button-text);
        box-shadow: var(--action-button-shadow);
        transition: background-color var(--transition-speed), transform var(--transition-speed);
    }

    .actions-section button:hover {
        background-color: rgba(0, 0, 0, 0.05); /* Light overlay on hover */
        transform: scale(1.05);
    }

    /* Flex layout for options */
    .options {
        display: flex;
        flex-wrap: wrap;
        gap: 15px;
        align-items: center;
    }

    .options label {
        font-size: 16px;
    }

    /* Character Bank Grid */
    #characterBank, #equationBank {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
        gap: 10px;
        max-height: 500px;
        overflow-y: auto;
    }

    #characterBank button {
        padding: 10px;
        font-size: 20px;
        border: 1px solid var(--border-color);
        border-radius: 6px;
        background-color: var(--symbol-color);
        color: #ffffff;
        transition: background-color var(--transition-speed), transform var(--transition-speed);
    }

    #characterBank button:hover {
        background-color: rgba(0, 128, 128, 0.8); /* Slightly darker teal on hover */
        transform: scale(1.05);
    }

    /* Equation Bank Grid */
    #equationBank button {
        padding: 10px;
        font-size: 16px;
        border: 1px solid var(--border-color);
        border-radius: 6px;
        background-color: var(--equation-color);
        color: #ffffff;
        transition: background-color var(--transition-speed), transform var(--transition-speed);
        text-align: center;
    }

    #equationBank button:hover {
        background-color: rgba(255, 87, 34, 0.8); /* Slightly darker orange on hover */
        transform: scale(1.05);
    }

    /* Custom Character and Equation Input */
    #customCharContainer, #customEqContainer {
        display: flex;
        gap: 10px;
        margin-top: 10px;
    }

    #customCharInput, #customEqInput {
        flex: 1;
        max-width: 200px;
    }

    /* Preview Section */
    #preview {
        padding: 15px;
        background-color: var(--background-color);
        font-size: 18px;
        border: 1px solid var(--border-color);
        min-height: 50px;
        margin-bottom: 20px;
        word-wrap: break-word;
        font-family: 'Open Sans', sans-serif;
        border-radius: 6px;
        display: none;
        transition: background-color var(--transition-speed), border-color var(--transition-speed);
    }

    /* Help Modal */
    #helpModal {
        display: none;
        position: fixed;
        z-index: 1000;
        padding-top: 60px;
        left: 0; top: 0;
        width: 100%; height: 100%;
        overflow: auto;
        background-color: rgba(0,0,0,0.6);
        transition: opacity var(--transition-speed);
    }

    #helpContent {
        background-color: var(--card-background);
        margin: 5% auto;
        padding: 30px;
        border: 1px solid var(--border-color);
        width: 90%;
        max-width: 700px;
        color: var(--text-color);
        border-radius: 8px;
        position: relative;
        box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        transition: background-color var(--transition-speed), color var(--transition-speed);
    }

    #helpContent h2 {
        margin-top: 0;
        color: var(--primary-color);
    }

    #closeHelp {
        position: absolute;
        top: 15px;
        right: 20px;
        font-size: 28px;
        font-weight: bold;
        color: var(--text-color);
        cursor: pointer;
        transition: color var(--transition-speed);
    }

    #closeHelp:hover {
        color: var(--error-color);
    }

    /* Search Bar */
    #charSearchInput, #eqSearchInput {
        width: 100%;
        padding: 10px 14px;
        margin-bottom: 15px;
        font-size: 16px;
        border: 1px solid var(--border-color);
        border-radius: 6px;
        box-sizing: border-box;
        transition: border-color var(--transition-speed);
    }

    #charSearchInput:focus, #eqSearchInput:focus {
        border-color: var(--primary-color);
        outline: none;
    }

    /* Font Size Slider */
    #fontSizeContainer {
        display: flex;
        align-items: center;
        gap: 10px;
        height: auto; /* Remove fixed height */
    }

    #fontSizeSlider {
        flex: 1;
    }

    /* Action Buttons Section */
    .actions-section {
        display: flex;
        flex-wrap: wrap;
        gap: 10px;
        justify-content: center;
    }

    /* Responsive Design */
    @media (max-width: 768px) {
        .options {
            flex-direction: column;
            align-items: flex-start;
        }

        .actions-section {
            flex-direction: column;
        }

        #characterBank, #equationBank {
            grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
        }
    }

    /* Utility Classes */
    .highlight {
        background-color: var(--error-color);
        color: #ffffff;
        border-radius: 4px;
        padding: 2px 4px;
    }
</style>

<div class="container">

    <h1>Subscript and Superscript Generator</h1>

    <!-- Input Section -->
    <div class="input-section">
        <label for="inputText">Enter your text:</label>
        <textarea id="inputText" rows="4" placeholder="Type or paste your text here..."></textarea>
    </div>

    <!-- Options Section -->
    <div class="options-section">
        <div class="options">
            <label><input type="radio" name="scriptType" value="subscript" checked> Subscript</label>
            <label><input type="radio" name="scriptType" value="superscript"> Superscript</label>
            <label><input type="checkbox" id="highlightUnsupported" checked> Highlight Unsupported Characters</label>
            <label><input type="checkbox" id="copyAsRichText"> Copy as Rich Text</label>
        </div>
    </div>

    <!-- Font Size Adjustment -->
    <div class="options-section">
        <label for="fontSizeSlider">Adjust Font Size:</label>
        <div id="fontSizeContainer">
            <input type="range" id="fontSizeSlider" min="12" max="36" value="18">
            <span id="fontSizeValue">18px</span>
        </div>
    </div>

    <!-- Output Section -->
    <div class="output-section">
        <label for="outputText">Converted text:</label>
        <textarea id="outputText" rows="4" readonly></textarea>
        <div id="preview"></div>
    </div>

    <!-- Action Buttons Section -->
    <div class="actions-section">
        <button id="undoButton">Undo</button>
        <button id="redoButton">Redo</button>
        <button id="copyButton">Copy to Clipboard</button>
        <button id="downloadButton">Download Text</button>
        <button id="clearButton">Clear</button>
        <button id="darkModeToggle">Toggle Dark Mode</button>
        <button id="helpButton">Help</button>
    </div>

    <!-- Character Bank Section -->
    <div class="character-bank-section">
        <label>Insert Symbol:</label>
        <!-- Search Field -->
        <input type="text" id="charSearchInput" placeholder="Search symbols...">
        <!-- Character Bank Grid -->
        <div id="characterBank">
            <!-- Greek Letters -->
            <button type="button" class="char-btn" title="Alpha">α</button>
            <button type="button" class="char-btn" title="Beta">β</button>
            <button type="button" class="char-btn" title="Gamma">γ</button>
            <button type="button" class="char-btn" title="Delta">Δ</button>
            <button type="button" class="char-btn" title="Epsilon">ε</button>
            <button type="button" class="char-btn" title="Theta">θ</button>
            <button type="button" class="char-btn" title="Lambda">λ</button>
            <button type="button" class="char-btn" title="Mu">μ</button>
            <button type="button" class="char-btn" title="Pi">π</button>
            <button type="button" class="char-btn" title="Sigma">σ</button>
            <button type="button" class="char-btn" title="Phi">φ</button>
            <button type="button" class="char-btn" title="Omega">Ω</button>
            <!-- Mathematical Symbols -->
            <button type="button" class="char-btn" title="Infinity">∞</button>
            <button type="button" class="char-btn" title="Summation">∑</button>
            <button type="button" class="char-btn" title="Product">∏</button>
            <button type="button" class="char-btn" title="Square Root">√</button>
            <button type="button" class="char-btn" title="Integral">∫</button>
            <button type="button" class="char-btn" title="Approximately Equal">≈</button>
            <button type="button" class="char-btn" title="Not Equal">≠</button>
            <button type="button" class="char-btn" title="Less Than or Equal To">≤</button>
            <button type="button" class="char-btn" title="Greater Than or Equal To">≥</button>
            <!-- Additional Mathematical Symbols -->
            <button type="button" class="char-btn" title="Partial Derivative">∂</button>
            <button type="button" class="char-btn" title="Nabla">∇</button>
            <button type="button" class="char-btn" title="Empty Set">∅</button>
            <button type="button" class="char-btn" title="Element Of">∈</button>
            <button type="button" class="char-btn" title="Not Element Of">∉</button>
            <button type="button" class="char-btn" title="Intersection">∩</button>
            <button type="button" class="char-btn" title="Union">∪</button>
            <button type="button" class="char-btn" title="Subset">⊂</button>
            <button type="button" class="char-btn" title="Superset">⊃</button>
            <button type="button" class="char-btn" title="Aleph">ℵ</button>
            <button type="button" class="char-btn" title="Plus-Minus">±</button>
            <button type="button" class="char-btn" title="Minus-Plus">∓</button>
            <button type="button" class="char-btn" title="Identical To">≡</button>
            <button type="button" class="char-btn" title="Right Arrow">→</button>
            <button type="button" class="char-btn" title="Left Arrow">←</button>
            <button type="button" class="char-btn" title="Left-Right Arrow">↔</button>
            <button type="button" class="char-btn" title="Implies">⇒</button>
            <button type="button" class="char-btn" title="If and Only If">⇔</button>
            <button type="button" class="char-btn" title="Real Numbers">ℝ</button>
            <button type="button" class="char-btn" title="Integers">ℤ</button>
            <button type="button" class="char-btn" title="Rational Numbers">ℚ</button>
            <button type="button" class="char-btn" title="Natural Numbers">ℕ</button>
            <button type="button" class="char-btn" title="Complex Numbers">ℂ</button>
        </div>
        <!-- Custom Character Input -->
        <div id="customCharContainer">
            <input type="text" id="customCharInput" placeholder="Add Symbol" maxlength="1">
            <button id="addCustomChar" style="background-color: var(--secondary-color);">Add</button>
        </div>
    </div>

    <!-- Equation Bank Section -->
   <div class="equation-bank-section">
    <label>Insert Equation:</label>
    <!-- Search Field -->
    <input type="text" id="eqSearchInput" placeholder="Search equations...">
    <!-- Equation Bank Grid -->
    <div id="equationBank">
      <button type="button" class="eq-btn" title="Quadratic Formula">x = [-b ± √(b²-4ac)]/(2a)</button>
        <button type="button" class="eq-btn" title="Pythagorean Theorem">a² + b² = c²</button>
        <button type="button" class="eq-btn" title="Euler's Formula">e^{iπ} + 1 = 0</button>
        <button type="button" class="eq-btn" title="Area of Circle">A = πr²</button>
        <button type="button" class="eq-btn" title="Volume of Sphere">V = (4/3)πr³</button>
        <button type="button" class="eq-btn" title="Slope of a Line">m = (y₂ - y₁)/(x₂ - x₁)</button>
        <button type="button" class="eq-btn" title="Derivative">f'(x) = lim_{h→0} [f(x+h) - f(x)] / h</button>
        <button type="button" class="eq-btn" title="Integral">∫f(x)dx</button>
        <button type="button" class="eq-btn" title="Binomial Theorem">(a + b)^n = Σ_{k=0}^n C(n,k)a^{n-k}b^k</button>
        <button type="button" class="eq-btn" title="Law of Cosines">c² = a² + b² - 2ab cos(C)</button>
        <button type="button" class="eq-btn" title="Einstein's Mass-Energy Equivalence">E = mc²</button>
        <button type="button" class="eq-btn" title="Circumference of Circle">C = 2πr</button>
        <button type="button" class="eq-btn" title="Distance Formula">d = √[(x₂-x₁)² + (y₂-y₁)²]</button>
        <button type="button" class="eq-btn" title="Area of Triangle">A = (1/2)bh</button>
        <button type="button" class="eq-btn" title="Vector Dot Product">a⋅b = |a||b|cos(θ)</button>
        <button type="button" class="eq-btn" title="Law of Sines">a/sin(A) = b/sin(B) = c/sin(C)</button>
        <button type="button" class="eq-btn" title="Ideal Gas Law">PV = nRT</button>
        <button type="button" class="eq-btn" title="Taylor Series">f(x) = Σ_{n=0}^∞ (f^{(n)}(a)/n!)(x-a)^n</button>
        <button type="button" class="eq-btn" title="Maxwell's First Equation">∇⋅E = ρ/ε₀</button>
        <button type="button" class="eq-btn" title="Schrödinger Equation">iℏ∂ψ/∂t = Ĥψ</button>
        <button type="button" class="eq-btn" title="Normal Distribution">f(x) = (1/σ√(2π))e^{-(x-μ)²/(2σ²)}</button>
        <button type="button" class="eq-btn" title="Wave Equation">∂²u/∂t² = c²∂²u/∂x²</button>
        <button type="button" class="eq-btn" title="Heat Equation">∂u/∂t = α∇²u</button>
        <button type="button" class="eq-btn" title="Euler's Identity">e^{iθ} = cos(θ) + isin(θ)</button>
        <button type="button" class="eq-btn" title="Area of Rectangle">A = l × w</button>
        <button type="button" class="eq-btn" title="Vector Cross Product">|a×b| = |a||b|sin(θ)</button>
        <button type="button" class="eq-btn" title="Fourier Transform">F(ω) = ∫_{-∞}^∞ f(t)e^{-iωt}dt</button>
        <button type="button" class="eq-btn" title="Laplace Transform">F(s) = ∫_{0}^∞ f(t)e^{-st}dt</button>
        <button type="button" class="eq-btn" title="Maxwell-Boltzmann Distribution">f(v) = √(m/2πkT)³ e^{-mv²/2kT}</button>
        <button type="button" class="eq-btn" title="Lorentz Factor">γ = 1/√(1-v²/c²)</button>
        <button type="button" class="eq-btn" title="Planck's Law">B(λ,T) = (2hc²/λ⁵)/(e^{hc/λkT} - 1)</button>
        <button type="button" class="eq-btn" title="Heisenberg Uncertainty">ΔxΔp ≥ ℏ/2</button>
        <button type="button" class="eq-btn" title="Gravitational Force">F = G(m₁m₂)/r²</button>
        <button type="button" class="eq-btn" title="Coulomb's Law">F = k(q₁q₂)/r²</button>
        <button type="button" class="eq-btn" title="Standard Deviation">σ = √(Σ(x-μ)²/N)</button>
        <button type="button" class="eq-btn" title="Momentum">p = mv</button>
        <button type="button" class="eq-btn" title="Kinetic Energy">KE = (1/2)mv²</button>
        <button type="button" class="eq-btn" title="Potential Energy">PE = mgh</button>
        <button type="button" class="eq-btn" title="Work">W = F⋅d</button>
        <button type="button" class="eq-btn" title="Power">P = W/t</button>
        <button type="button" class="eq-btn" title="Ohm's Law">V = IR</button>
        <button type="button" class="eq-btn" title="Capacitance">C = Q/V</button>
        <button type="button" class="eq-btn" title="Inductance">V = L(dI/dt)</button>
        <button type="button" class="eq-btn" title="Magnetic Field">B = μ₀I/(2πr)</button>
        <button type="button" class="eq-btn" title="Wave Function">λ = v/f</button>
        <button type="button" class="eq-btn" title="Stefan-Boltzmann Law">P = σAT⁴</button>
        <button type="button" class="eq-btn" title="de Broglie Wavelength">λ = h/p</button>
        <button type="button" class="eq-btn" title="Bernoulli's Equation">P + (1/2)ρv² + ρgh = constant</button>
        <button type="button" class="eq-btn" title="Van der Waals Equation">(P + an²/V²)(V - nb) = nRT</button>
        <button type="button" class="eq-btn" title="Entropy Change">ΔS = Q/T</button>
        <button type="button" class="eq-btn" title="Specific Heat Formula">q = mcΔT</button>
        <button type="button" class="eq-btn" title="Snell's Law">n₁sinθ₁ = n₂sinθ₂</button>
        <button type="button" class="eq-btn" title="Hooke's Law">F = -kx</button>
        <button type="button" class="eq-btn" title="Ampère's Law">∮B⋅dl = μ₀I</button>
        <button type="button" class="eq-btn" title="Gibbs Free Energy">ΔG = ΔH - TΔS</button>
        <button type="button" class="eq-btn" title="Boyle's Law">P₁V₁ = P₂V₂</button>
        <button type="button" class="eq-btn" title="Charles's Law">V₁/T₁ = V₂/T₂</button>
        <button type="button" class="eq-btn" title="Magnetic Flux">Φ = B⋅A⋅cosθ</button>
        <button type="button" class="eq-btn" title="Photoelectric Effect">E_k = hf - φ</button>
        <button type="button" class="eq-btn" title="Moment of Inertia">I = Σmr²</button>
        <button type="button" class="eq-btn" title="Centripetal Force">F = mv²/r</button>
        <button type="button" class="eq-btn" title="Doppler Effect (frequency)">f' = f(v ± v₀)/(v ∓ vs)</button>
        <button type="button" class="eq-btn" title="Escape Velocity">v_e = √(2GM/r)</button>
        <button type="button" class="eq-btn" title="Thermal Efficiency">η = 1 - T_c/T_h</button>
        <button type="button" class="eq-btn" title="Ideal Transformer Equation">V₁/V₂ = N₁/N₂</button>
        <button type="button" class="eq-btn" title="Bohr's Radius">a₀ = 4πε₀ℏ²/(mₑe²)</button>
        <button type="button" class="eq-btn" title="Relativistic Energy">E² = (pc)² + (mc²)²</button>
        <button type="button" class="eq-btn" title="Chemical Equilibrium Constant">K = [C]^c[D]^d / [A]^a[B]^b</button>
        <button type="button" class="eq-btn" title="Frequency of a Pendulum">f = (1/2π)√(g/L)</button>
        <button type="button" class="eq-btn" title="Fermat's Last Theorem">xⁿ + yⁿ ≠ zⁿ, n > 2</button>
        <button type="button" class="eq-btn" title="Combined Gas Law">P₁V₁/T₁ = P₂V₂/T₂</button>
        <button type="button" class="eq-btn" title="Angular Momentum">L = Iω</button>
        <button type="button" class="eq-btn" title="Root Mean Square Speed">v_rms = √(3kT/m)</button>
        <button type="button" class="eq-btn" title="Gravitational Potential Energy">U = -G(m₁m₂)/r</button>
        <button type="button" class="eq-btn" title="Electrical Potential Energy">U = k(q₁q₂)/r</button>
        <button type="button" class="eq-btn" title="Kepler's Third Law">T² ∝ r³</button>
        <button type="button" class="eq-btn" title="Poisson's Equation">∇²φ = -ρ/ε₀</button>
        <button type="button" class="eq-btn" title="Thermodynamic Work">W = -PΔV</button>
        <button type="button" class="eq-btn" title="Rydberg Formula">1/λ = R_H(1/n₁² - 1/n₂²)</button>
        <button type="button" class="eq-btn" title="Relativistic Mass">m = m₀/√(1 - v²/c²)</button>
        <button type="button" class="eq-btn" title="Energy Stored in a Capacitor">U = (1/2)CV²</button>
        <button type="button" class="eq-btn" title="Magnetic Force on a Moving Charge">F = q(v × B)</button>
        <button type="button" class="eq-btn" title="Faraday's Law of Induction">ε = -dΦ/dt</button>
        <button type="button" class="eq-btn" title="Reynolds Number">Re = ρvL/μ</button>
        <button type="button" class="eq-btn" title="Hydrostatic Pressure">P = ρgh</button>
        <button type="button" class="eq-btn" title="Electric Field of a Point Charge">E = kq/r²</button>
        <button type="button" class="eq-btn" title="Drift Velocity">v_d = I/nqA</button>
        <button type="button" class="eq-btn" title="Molarity">M = n/V</button>
        <button type="button" class="eq-btn" title="Half-Life">N = N₀e^{-λt}</button>
        <button type="button" class="eq-btn" title="Arrhenius Equation">k = Ae^{-Ea/(RT)}</button>
        <button type="button" class="eq-btn" title="Logistic Growth">P(t) = K / (1 + e^{-r(t-t₀)})</button>
        <button type="button" class="eq-btn" title="Bragg's Law">nλ = 2d sinθ</button>
        <button type="button" class="eq-btn" title="Photon Energy">E = hf</button>
        <button type="button" class="eq-btn" title="Lens Maker's Formula">1/f = (n - 1)(1/R₁ - 1/R₂)</button>
        <button type="button" class="eq-btn" title="Quantum Uncertainty Principle">ΔEΔt ≥ ℏ/2</button>
        <button type="button" class="eq-btn" title="Rayleigh Criterion">θ = 1.22λ/D</button>
        <button type="button" class="eq-btn" title="Thermal Conductivity">Q = kAΔT/L</button>
        <button type="button" class="eq-btn" title="Moment of Force">τ = rFsinθ</button>
        <button type="button" class="eq-btn" title="Relative Velocity">v_{AB} = v_A - v_B</button>
        <button type="button" class="eq-btn" title="Decay Constant">λ = ln(2)/t₁/₂</button>
        <button type="button" class="eq-btn" title="Harmonic Oscillator Energy">E = (n + 1/2)ℏω</button>
        <button type="button" class="eq-btn" title="Mechanical Advantage">MA = F_out/F_in</button>
        <button type="button" class="eq-btn" title="Magnification">M = -di/do</button>
        <button type="button" class="eq-btn" title="Young's Modulus">E = σ/ε</button>
        <button type="button" class="eq-btn" title="Center of Mass">R = (Σmᵢrᵢ)/(Σmᵢ)</button>
        <button type="button" class="eq-btn" title="Mole Fraction">χₐ = nₐ/n_total</button>
        <button type="button" class="eq-btn" title="Clausius-Clapeyron Equation">ln(P₂/P₁) = -ΔHvap/R(1/T₂ - 1/T₁)</button>
        <button type="button" class="eq-btn" title="Power in AC Circuit">P = VIcosθ</button>
        <button type="button" class="eq-btn" title="Angular Frequency">ω = 2πf</button>
        <button type="button" class="eq-btn" title="Hubble's Law">v = H₀d</button>
        <button type="button" class="eq-btn" title="Friction Force">f = μN</button>
        <button type="button" class="eq-btn" title="Gravitational Field Strength">g = GM/r²</button>
        <button type="button" class="eq-btn" title="Relative Humidity">RH = (actual vapor pressure/saturation vapor pressure) × 100%</button>
        <button type="button" class="eq-btn" title="Electrostatic Potential Energy">U = qV</button>
        <button type="button" class="eq-btn" title="Photon Momentum">p = E/c</button>
        <button type="button" class="eq-btn" title="Beat Frequency">f_beat = |f₁ - f₂|</button>
        <button type="button" class="eq-btn" title="Magnetic Flux Linkage">λ = NΦ</button>
        <button type="button" class="eq-btn" title="Gibbs Phase Rule">F = C - P + 2</button>
        <button type="button" class="eq-btn" title="Harmonic Series Sum">S = Σ_{n=1}^∞ (1/n)</button>
        <button type="button" class="eq-btn" title="Electromagnetic Wave Equation">∇²E = μ₀ε₀ ∂²E/∂t²</button>
        <button type="button" class="eq-btn" title="Buckingham Pi Theorem">π₁ = f(π₂, π₃, ...)</button>
        <button type="button" class="eq-btn" title="Larmor Formula">P = (2/3)(q²a²)/(4πε₀c³)</button>
        <button type="button" class="eq-btn" title="Time Dilation">Δt' = Δt/√(1 - v²/c²)</button>
        <button type="button" class="eq-btn" title="Einstein Field Equation">R_{μν} - (1/2)Rg_{μν} + Λg_{μν} = (8πG/c⁴)T_{μν}</button>
        <button type="button" class="eq-btn" title="Surface Area of a Sphere">A = 4πr²</button>
        <button type="button" class="eq-btn" title="Spherical Harmonics">Y(θ, φ) = √((2l+1)/(4π)(l-m)!/(l+m)!)P(θ)e^{imφ}</button>
        <button type="button" class="eq-btn" title="Wein's Displacement Law">λ_max = b/T</button>
        <button type="button" class="eq-btn" title="Lorentz Transformation">x' = γ(x - vt)</button>
        <button type="button" class="eq-btn" title="Elastic Collision Equation">v₁' = (m₁ - m₂)v₁ + 2m₂v₂ / (m₁ + m₂)</button>
        <button type="button" class="eq-btn" title="Triple Product Expansion">a ⋅ (b × c) = (a × b) ⋅ c</button>
        <button type="button" class="eq-btn" title="Fundamental Frequency">f₀ = v/2L</button>
        <button type="button" class="eq-btn" title="Fourier Series">f(x) = a₀/2 + Σ(aₙcos(nx) + bₙsin(nx))</button>
        <button type="button" class="eq-btn" title="Moment of Inertia for a Solid Cylinder">I = (1/2)MR²</button>
        <button type="button" class="eq-btn" title="Center of Mass for Continuous Mass">R_cm = (1/M)∫r dm</button>
        <button type="button" class="eq-btn" title="Chain Rule in Calculus">dy/dx = (dy/du)(du/dx)</button>
        <button type="button" class="eq-btn" title="Wave Number">k = 2π/λ</button>
        <button type="button" class="eq-btn" title="Thermodynamic Free Energy">F = U - TS</button>
        <button type="button" class="eq-btn" title="Brewster's Angle">tanθ_B = n₂/n₁</button>
        <button type="button" class="eq-btn" title="Adiabatic Process (PV Relation)">P₁V₁^γ = P₂V₂^γ</button>
        <button type="button" class="eq-btn" title="Phase Velocity">v_p = ω/k</button>
        <button type="button" class="eq-btn" title="Impulse">J = FΔt</button>
        <button type="button" class="eq-btn" title="Vector Magnitude">|v| = √(v_x² + v_y² + v_z²)</button>
        <button type="button" class="eq-btn" title="Lagrangian">L = T - V</button>
        <button type="button" class="eq-btn" title="Second Law of Thermodynamics">ΔS ≥ 0</button>
        <button type="button" class="eq-btn" title="Total Internal Reflection">θ > θ_c = sin⁻¹(n₂/n₁)</button>
        <button type="button" class="eq-btn" title="Pressure-Volume Work">W = ∫PdV</button>
        <button type="button" class="eq-btn" title="Quantum Partition Function">Z = Σ e^{-E_i/kT}</button>
        <button type="button" class="eq-btn" title="Thermodynamic Efficiency">η = W/Q_in</button>
        <button type="button" class="eq-btn" title="Moment of Inertia for a Hollow Sphere">I = (2/3)MR²</button>
        <button type="button" class="eq-btn" title="Gravitational Potential">V = -GM/r</button>
        <button type="button" class="eq-btn" title="Schwarzschild Radius">r_s = 2GM/c²</button>
        <button type="button" class="eq-btn" title="Bulk Modulus">B = -V(ΔP/ΔV)</button>
        <button type="button" class="eq-btn" title="Heat Capacity">C = q/ΔT</button>
        <button type="button" class="eq-btn" title="Gradient in Cylindrical Coordinates">∇ = ∂/∂r eᵣ + (1/r)∂/∂θ e_θ + ∂/∂z e_z</button>
        <button type="button" class="eq-btn" title="Max Planck's Equation">E = nhν</button>
        <button type="button" class="eq-btn" title="Biot-Savart Law">dB = (μ₀/4π) * (I dl × r̂)/r²</button>
        <button type="button" class="eq-btn" title="Euler's Theorem">e^{iπ} = -1</button>
        <button type="button" class="eq-btn" title="Tangent Line Equation">y - y₁ = m(x - x₁)</button>
        <button type="button" class="eq-btn" title="Polar Form of Complex Number">z = r(cosθ + isinθ)</button>
        <button type="button" class="eq-btn" title="Mean Free Path">λ = 1/(√2 nσ)</button>
        <button type="button" class="eq-btn" title="Quantum Harmonic Oscillator">Eₙ = (n + 1/2)ℏω</button>
        <button type="button" class="eq-btn" title="Double Angle Formula for Sine">sin(2θ) = 2sinθcosθ</button>
        <button type="button" class="eq-btn" title="Sum of Interior Angles">Σθ = (n-2) × 180°</button>
        <button type="button" class="eq-btn" title="Angular Displacement">θ = s/r</button>
        <button type="button" class="eq-btn" title="Fick's First Law of Diffusion">J = -D(dC/dx)</button>
        <button type="button" class="eq-btn" title="Relative Atomic Mass">Ar = m_avg/m_u</button>
        <button type="button" class="eq-btn" title="Binomial Probability Formula">P(X = k) = C(n, k)p^k(1 - p)^(n - k)</button>
        <button type="button" class="eq-btn" title="Distance Between Two Points">d = √((x₂ - x₁)² + (y₂ - y₁)²)</button>
        <button type="button" class="eq-btn" title="Kinematic Equation (No Time)">v² = u² + 2as</button>
        <button type="button" class="eq-btn" title="Geometric Series Sum">S_n = a(1 - r^n)/(1 - r)</button>
        <button type="button" class="eq-btn" title="Heron's Formula">A = √(s(s - a)(s - b)(s - c))</button>
        <button type="button" class="eq-btn" title="Stefan's Law of Black Body Radiation">P = σAT⁴</button>
        <button type="button" class="eq-btn" title="Bode's Law (Planetary Distances)">d = 0.4 + 0.3 × 2^n (n = -∞, 0, 1, 2,...)</button>
        <button type="button" class="eq-btn" title="Gaussian Distribution Formula">f(x) = (1/σ√(2π))e^(-(x - μ)²/(2σ²))</button>
        <button type="button" class="eq-btn" title="Newton's Law of Cooling">T(t) = T_env + (T₀ - T_env)e^(-kt)</button>
        <button type="button" class="eq-btn" title="Standard Error of the Mean">SE = σ/√n</button>
        <button type="button" class="eq-btn" title="De Moivre's Theorem">(cos θ + i sin θ)^n = cos(nθ) + i sin(nθ)</button>
        <button type="button" class="eq-btn" title="Critical Angle">θ_c = sin⁻¹(n₂/n₁)</button>
        <button type="button" class="eq-btn" title="Bond Energy">ΔH ≈ Σ(bonds broken) - Σ(bonds formed)</button>
        <button type="button" class="eq-btn" title="Geometric Mean">GM = (Πxᵢ)^(1/n)</button>
        <button type="button" class="eq-btn" title="Average Velocity">v_avg = (v₁ + v₂)/2</button>
        <button type="button" class="eq-btn" title="Second Moment of Area for a Rectangle">I = (bh³)/12</button>
        <button type="button" class="eq-btn" title="Continuity Equation">A₁v₁ = A₂v₂</button>
        <button type="button" class="eq-btn" title="Parabolic Motion (Range)">R = (v₀² sin 2θ)/g</button>
        <button type="button" class="eq-btn" title="Hyperbolic Identity">cosh²(x) - sinh²(x) = 1</button>
        <button type="button" class="eq-btn" title="Algebraic Mean">AM = (Σxᵢ)/n</button>
        <button type="button" class="eq-btn" title="Moment of Inertia for a Point Mass">I = mr²</button>
        <button type="button" class="eq-btn" title="Poisson Distribution">P(X=k) = (λ^k e^(-λ))/k!</button>
        <button type="button" class="eq-btn" title="Law of Tangents">((a - b)/(a + b)) = ((tan((A - B)/2))/(tan((A + B)/2)))</button>
        <button type="button" class="eq-btn" title="Hess's Law">ΔH = ΣΔH(products) - ΣΔH(reactants)</button>
        <button type="button" class="eq-btn" title="Parallel Plate Capacitance">C = ε₀A/d</button>
        <button type="button" class="eq-btn" title="Ideal Mechanical Advantage">IMA = d_in/d_out</button>
        <button type="button" class="eq-btn" title="VSEPR Theory (Electron Pair Geometry)">AXₙEₘ</button>
        <button type="button" class="eq-btn" title="Radiant Flux">Φ = ∫I(θ) dA</button>
        <button type="button" class="eq-btn" title="Hydrostatic Equilibrium Equation">dP/dr = -Gρ(r)m(r)/r²</button>
        <button type="button" class="eq-btn" title="Nyquist Theorem">f_s ≥ 2f_max</button>
        <button type="button" class="eq-btn" title="Coefficient of Linear Expansion">ΔL = αL₀ΔT</button>
        <button type="button" class="eq-btn" title="Coefficient of Performance (Refrigerator)">COP = Q_c/W</button>
        <button type="button" class="eq-btn" title="Marginal Cost">MC = ΔTC/ΔQ</button>
        <button type="button" class="eq-btn" title="Relative Velocity in Relativity">v_rel = (v₁ + v₂)/(1 + v₁v₂/c²)</button>
        <button type="button" class="eq-btn" title="Molar Mass">M = m/n</button>
        <button type="button" class="eq-btn" title="Maclaurin Series">f(x) = Σ (f⁽ⁿ⁾(0)/n!)xⁿ</button>
        <button type="button" class="eq-btn" title="Risk Premium">Risk Premium = Expected Return - Risk-Free Rate</button>
        <button type="button" class="eq-btn" title="Van't Hoff Equation">ln(K₂/K₁) = -ΔH/R(1/T₂ - 1/T₁)</button>
        <button type="button" class="eq-btn" title="Impulse-Momentum Theorem">J = Δp</button>
        <button type="button" class="eq-btn" title="Volume of a Cone">V = (1/3)πr²h</button>
        <button type="button" class="eq-btn" title="Coulomb's Law for Continuous Charge Distribution">E = (1/4πε₀) ∫ (dq/r²) r̂</button>
        <button type="button" class="eq-btn" title="Lorentz Force Law">F = q(E + v × B)</button>
        <button type="button" class="eq-btn" title="Orbital Velocity">v = √(GM/r)</button>
        <button type="button" class="eq-btn" title="Stirling's Approximation">n! ≈ √(2πn)(n/e)ⁿ</button>
        <button type="button" class="eq-btn" title="Length Contraction">L = L₀√(1 - v²/c²)</button>
        <button type="button" class="eq-btn" title="Mach Number">M = v/a</button>
        <button type="button" class="eq-btn" title="Coefficient of Kinetic Friction">f_k = μ_kN</button>
        <button type="button" class="eq-btn" title="Moment of Inertia of a Rod about Its End">I = (1/3)ML²</button>
        <button type="button" class="eq-btn" title="Wavelength of Light in a Medium">λ_medium = λ₀/n</button>
        <button type="button" class="eq-btn" title="Diffraction Grating Formula">d sin θ = mλ</button>
        <button type="button" class="eq-btn" title="Maxwell Relation (Thermodynamics)">(∂S/∂V)_T = (∂P/∂T)_V</button>
        <button type="button" class="eq-btn" title="Euler's Criterion (for Primality)">a^(p-1) ≡ 1 (mod p)</button>
        <button type="button" class="eq-btn" title="Pressure Gradient Force">F = -∇P</button>
    </div>
    <!-- Custom Equation Input -->
    <div id="customEqContainer">
        <input type="text" id="customEqInput" placeholder="Add Equation">
        <button id="addCustomEq" style="background-color: var(--secondary-color);">Add</button>
    </div>
</div>

    <!-- Help Modal -->
    <div id="helpModal">
        <div id="helpContent">
            <span id="closeHelp">&times;</span>
            <h2>How to Use Subscript and Superscript Generator</h2>
            <p>Enter your text in the input area and select whether you want to convert it to subscript or superscript.</p>
            <p>Use the character bank to insert Greek letters and mathematical symbols into your text. You can search for symbols using the search bar.</p>
            <p>Use the equation bank to insert common mathematical equations into your text. Search for equations using the search bar.</p>
            <p>You can also add custom characters or equations to their respective banks using the input fields provided. Custom entries are saved and will be available next time you visit.</p>
            <p>Adjust the font size using the slider to increase or decrease the size of the preview and output text.</p>
            <p>The converted text will appear in the "Converted text" box below, and you can copy it to your clipboard or download it as a text file.</p>
            <p>Use the "Highlight Unsupported Characters" option to identify characters that cannot be converted.</p>
            <p>Toggle dark mode for a different visual experience.</p>
            <p>Use the "Copy as Rich Text" option to copy the formatted text, preserving superscripts and subscripts when pasting into word processors.</p>
            <p>The Undo and Redo buttons allow you to revert changes in your input text.</p>
        </div>
    </div>

</div>

<script>
    // Subscript and Superscript characters mapping
    const charMap = {
        subscript: {
            // Numbers
            '0': '₀', '1': '₁', '2': '₂', '3': '₃', '4': '₄',
            '5': '₅', '6': '₆', '7': '₇', '8': '₈', '9': '₉',
            // Latin letters
            'a': 'ₐ', 'e': 'ₑ', 'h': 'ₕ', 'i': 'ᵢ', 'j': 'ⱼ',
            'k': 'ₖ', 'l': 'ₗ', 'm': 'ₘ', 'n': 'ₙ', 'o': 'ₒ',
            'p': 'ₚ', 'r': 'ᵣ', 's': 'ₛ', 't': 'ₜ', 'u': 'ᵤ',
            'v': 'ᵥ', 'x': 'ₓ',
            // Greek letters
            'α': 'ᵦ', 'β': 'ᵦ', 'γ': 'ᵧ', 'δ': 'ᵟ', 'ε': 'ₑ',
            'θ': 'ᶿ', 'λ': 'ᶥ', 'μ': 'ᵤ', 'π': 'ᵨ', 'ρ': 'ᵨ',
            'σ': 'ᵩ', 'φ': 'ᵩ', 'ω': 'ᵡ',
            // Mathematical symbols
            '+': '₊', '-': '₋', '=': '₌', '(': '₍', ')': '₎',
            // Uppercase letters mapped to lowercase equivalents if possible
            'A': 'ₐ', 'E': 'ₑ', 'H': 'ₕ', 'I': 'ᵢ', 'J': 'ⱼ',
            'K': 'ₖ', 'L': 'ₗ', 'M': 'ₘ', 'N': 'ₙ', 'O': 'ₒ',
            'P': 'ₚ', 'R': 'ᵣ', 'S': 'ₛ', 'T': 'ₜ', 'U': 'ᵤ',
            'V': 'ᵥ', 'X': 'ₓ',
        },
        superscript: {
            // Numbers
            '0': '⁰', '1': '¹', '2': '²', '3': '³', '4': '⁴',
            '5': '⁵', '6': '⁶', '7': '⁷', '8': '⁸', '9': '⁹',
            // Latin letters
            'a': 'ᵃ', 'b': 'ᵇ', 'c': 'ᶜ', 'd': 'ᵈ', 'e': 'ᵉ',
            'f': 'ᶠ', 'g': 'ᵍ', 'h': 'ʰ', 'i': 'ⁱ', 'j': 'ʲ',
            'k': 'ᵏ', 'l': 'ˡ', 'm': 'ᵐ', 'n': 'ⁿ', 'o': 'ᵒ',
            'p': 'ᵖ', 'r': 'ʳ', 's': 'ˢ', 't': 'ᵗ', 'u': 'ᵘ',
            'v': 'ᵛ', 'w': 'ʷ', 'x': 'ˣ', 'y': 'ʸ', 'z': 'ᶻ',
            // Greek letters
            'α': 'ᵝ', 'β': 'ᵝ', 'γ': 'ᵞ', 'δ': 'ᵟ', 'ε': 'ᵋ',
            'θ': 'ᶿ', 'λ': 'ᶢ', 'μ': 'ᶮ', 'π': 'ᵠ', 'ρ': 'ʳ',
            'σ': 'ˢ', 'φ': 'ᵠ', 'ω': 'ᵚ',
            // Mathematical symbols
            '+': '⁺', '-': '⁻', '=': '⁼', '(': '⁽', ')': '⁾',
            // Uppercase letters
            'A': 'ᴬ', 'B': 'ᴮ', 'C': 'ᶜ', 'D': 'ᴰ', 'E': 'ᴱ',
            'F': 'ᶠ', 'G': 'ᴳ', 'H': 'ᴴ', 'I': 'ᴵ', 'J': 'ᴶ',
            'K': 'ᴷ', 'L': 'ᴸ', 'M': 'ᴹ', 'N': 'ᴺ', 'O': 'ᴼ',
            'P': 'ᴾ', 'R': 'ᴿ', 'S': 'ˢ', 'T': 'ᵀ', 'U': 'ᵁ',
            'V': 'ⱽ', 'W': 'ᵂ',
        }
    };

    // Symbol descriptions for search functionality
    const symbolDescriptions = {
        'α': 'Alpha',
        'β': 'Beta',
        'γ': 'Gamma',
        'Δ': 'Delta',
        'ε': 'Epsilon',
        'θ': 'Theta',
        'λ': 'Lambda',
        'μ': 'Mu',
        'π': 'Pi',
        'σ': 'Sigma',
        'φ': 'Phi',
        'Ω': 'Omega',
        '∞': 'Infinity',
        '∑': 'Summation',
        '∏': 'Product',
        '√': 'Square Root',
        '∫': 'Integral',
        '≈': 'Approximately Equal',
        '≠': 'Not Equal',
        '≤': 'Less Than or Equal To',
        '≥': 'Greater Than or Equal To',
        '∂': 'Partial Derivative',
        '∇': 'Nabla',
        '∅': 'Empty Set',
        '∈': 'Element Of',
        '∉': 'Not Element Of',
        '∩': 'Intersection',
        '∪': 'Union',
        '⊂': 'Subset',
        '⊃': 'Superset',
        'ℵ': 'Aleph',
        '±': 'Plus-Minus',
        '∓': 'Minus-Plus',
        '≡': 'Identical To',
        '→': 'Right Arrow',
        '←': 'Left Arrow',
        '↔': 'Left-Right Arrow',
        '⇒': 'Implies',
        '⇔': 'If and Only If',
        'ℝ': 'Real Numbers',
        'ℤ': 'Integers',
        'ℚ': 'Rational Numbers',
        'ℕ': 'Natural Numbers',
        'ℂ': 'Complex Numbers',
    };

    // Equation descriptions for search functionality
    const equationDescriptions = {
        'x = [-b ± √(b²-4ac)]/(2a)': 'Quadratic Formula',
        'a² + b² = c²': 'Pythagorean Theorem',
        'e^{iπ} + 1 = 0': "Euler's Formula",
        'A = πr²': 'Area of Circle',
        'V = (4/3)πr³': 'Volume of Sphere',
        'm = (y₂ - y₁)/(x₂ - x₁)': 'Slope of a Line',
        "f'(x) = lim_{h→0} [f(x+h) - f(x)] / h": 'Derivative',
        '∫f(x)dx': 'Integral',
        '(a + b)^n = Σ_{k=0}^n C(n,k)a^{n-k}b^k': 'Binomial Theorem',
        'c² = a² + b² - 2ab cos(C)': 'Law of Cosines',
    };

    // DOM Content Loaded Event
    document.addEventListener('DOMContentLoaded', function() {
        // Get elements
        const inputText = document.getElementById('inputText');
        const outputText = document.getElementById('outputText');
        const copyButton = document.getElementById('copyButton');
        const clearButton = document.getElementById('clearButton');
        const downloadButton = document.getElementById('downloadButton');
        const scriptTypeRadios = document.getElementsByName('scriptType');
        const darkModeToggle = document.getElementById('darkModeToggle');
        const highlightUnsupported = document.getElementById('highlightUnsupported');
        const fontSizeSlider = document.getElementById('fontSizeSlider');
        const fontSizeValue = document.getElementById('fontSizeValue');
        const characterBank = document.getElementById('characterBank');
        const charButtons = document.querySelectorAll('.char-btn');
        const customCharInput = document.getElementById('customCharInput');
        const addCustomChar = document.getElementById('addCustomChar');
        const helpButton = document.getElementById('helpButton');
        const helpModal = document.getElementById('helpModal');
        const closeHelp = document.getElementById('closeHelp');
        const charSearchInput = document.getElementById('charSearchInput');
        const copyAsRichText = document.getElementById('copyAsRichText');
        const undoButton = document.getElementById('undoButton');
        const redoButton = document.getElementById('redoButton');
        const preview = document.getElementById('preview');
        const equationBank = document.getElementById('equationBank');
        const eqSearchInput = document.getElementById('eqSearchInput');
        const customEqInput = document.getElementById('customEqInput');
        const addCustomEq = document.getElementById('addCustomEq');

        let undoStack = [];
        let redoStack = [];

        // Initialize undoStack with initial input value
        undoStack.push(inputText.value);

        // Function to convert text
        function convertText() {
            let scriptType = document.querySelector('input[name="scriptType"]:checked').value;
            let result = '';
            let plainResult = '';
            let formattedResult = '';

            for (let char of inputText.value) {
                let convertedChar = charMap[scriptType][char];
                if (convertedChar) {
                    result += convertedChar;
                    plainResult += convertedChar;
                    formattedResult += convertedChar;
                } else {
                    if (highlightUnsupported.checked) {
                        // Highlight unsupported character
                        result += char;
                        plainResult += char;
                        formattedResult += `<span class="highlight" title="Unsupported Character: ${char}">${char}</span>`;
                    } else {
                        // Use original character
                        result += char;
                        plainResult += char;
                        formattedResult += char;
                    }
                }
            }

            outputText.value = plainResult;
            // Display formatted text in preview
            preview.innerHTML = formattedResult;
            preview.style.display = 'block';
        }

        // Event listeners
        inputText.addEventListener('input', () => {
            // Save the current value to undo stack
            undoStack.push(inputText.value);
            // Clear the redo stack
            redoStack = [];
            convertText();
        });

        scriptTypeRadios.forEach(radio => {
            radio.addEventListener('change', convertText);
        });

        highlightUnsupported.addEventListener('change', convertText);

        // Adjust font size
        fontSizeSlider.addEventListener('input', () => {
            const fontSize = fontSizeSlider.value + 'px';
            outputText.style.fontSize = fontSize;
            preview.style.fontSize = fontSize;
            fontSizeValue.textContent = fontSize;
            // Save font size to local storage
            localStorage.setItem('fontSize', fontSize);
        });

        // Load font size from local storage
        const savedFontSize = localStorage.getItem('fontSize');
        if (savedFontSize) {
            fontSizeSlider.value = parseInt(savedFontSize);
            outputText.style.fontSize = savedFontSize;
            preview.style.fontSize = savedFontSize;
            fontSizeValue.textContent = savedFontSize;
        } else {
            fontSizeValue.textContent = fontSizeSlider.value + 'px';
        }

        // Character bank insertion
        charButtons.forEach(button => {
            button.addEventListener('click', () => {
                inputText.value += button.textContent;
                convertText();
                inputText.focus();
            });
        });

        // Load custom characters from local storage
        const customChars = JSON.parse(localStorage.getItem('customChars')) || [];

        // Function to add a character button
        function addCharButton(char) {
            const newButton = document.createElement('button');
            newButton.type = 'button';
            newButton.className = 'char-btn';
            newButton.textContent = char;
            newButton.title = symbolDescriptions[char] || 'Custom Symbol';
            characterBank.appendChild(newButton);
            newButton.addEventListener('click', () => {
                inputText.value += newButton.textContent;
                convertText();
                inputText.focus();
            });
        }

        // Add existing custom characters
        customChars.forEach(char => {
            addCharButton(char);
        });

        // Add custom character to character bank
        addCustomChar.addEventListener('click', () => {
            const customChar = customCharInput.value.trim();
            if (customChar && !customChars.includes(customChar)) {
                addCharButton(customChar);
                customChars.push(customChar);
                localStorage.setItem('customChars', JSON.stringify(customChars));
                customCharInput.value = '';
            } else if (customChars.includes(customChar)) {
                alert('Character already exists in the character bank.');
            }
        });

        // Equation Bank insertion
        const eqButtons = equationBank.querySelectorAll('.eq-btn');

        // Load custom equations from local storage
        const customEqs = JSON.parse(localStorage.getItem('customEqs')) || [];

        // Function to add an equation button
        function addEqButton(eq) {
            const newButton = document.createElement('button');
            newButton.type = 'button';
            newButton.className = 'eq-btn';
            newButton.textContent = eq;
            newButton.title = equationDescriptions[eq] || 'Custom Equation';
            equationBank.appendChild(newButton);
            newButton.addEventListener('click', () => {
                inputText.value += eq;
                convertText();
                inputText.focus();
            });
        }

        // Add existing custom equations
        customEqs.forEach(eq => {
            addEqButton(eq);
        });

        // Add common equations (initial)
        eqButtons.forEach(button => {
            button.addEventListener('click', () => {
                inputText.value += button.textContent;
                convertText();
                inputText.focus();
            });
        });

        // Add custom equation to equation bank
        addCustomEq.addEventListener('click', () => {
            const customEq = customEqInput.value.trim();
            if (customEq && !customEqs.includes(customEq)) {
                addEqButton(customEq);
                customEqs.push(customEq);
                localStorage.setItem('customEqs', JSON.stringify(customEqs));
                customEqInput.value = '';
            } else if (customEqs.includes(customEq)) {
                alert('Equation already exists in the equation bank.');
            }
        });

        // Search functionality for character bank
        charSearchInput.addEventListener('input', () => {
            const searchTerm = charSearchInput.value.toLowerCase();
            document.querySelectorAll('.char-btn').forEach(button => {
                const symbol = button.textContent;
                const description = symbolDescriptions[symbol] || '';
                if (symbol.toLowerCase().includes(searchTerm) || description.toLowerCase().includes(searchTerm)) {
                    button.style.display = 'block';
                } else {
                    button.style.display = 'none';
                }
            });
        });

        // Search functionality for equation bank
        eqSearchInput.addEventListener('input', () => {
            const searchTerm = eqSearchInput.value.toLowerCase();
            document.querySelectorAll('.eq-btn').forEach(button => {
                const eq = button.textContent;
                const description = equationDescriptions[eq] || '';
                if (eq.toLowerCase().includes(searchTerm) || description.toLowerCase().includes(searchTerm)) {
                    button.style.display = 'block';
                } else {
                    button.style.display = 'none';
                }
            });
        });

        // Copy to clipboard
        copyButton.addEventListener('click', () => {
            if (copyAsRichText.checked) {
                // Copy as rich text using the preview
                const tempElem = document.createElement('div');
                tempElem.innerHTML = preview.innerHTML;
                document.body.appendChild(tempElem);

                const selection = window.getSelection();
                const range = document.createRange();
                range.selectNodeContents(tempElem);
                selection.removeAllRanges();
                selection.addRange(range);

                try {
                    document.execCommand('copy');
                    alert('Converted text copied to clipboard as rich text!');
                } catch (err) {
                    alert('Failed to copy text: ' + err);
                }

                selection.removeAllRanges();
                document.body.removeChild(tempElem);
            } else {
                // Copy as plain text
                navigator.clipboard.writeText(outputText.value)
                    .then(() => {
                        alert('Converted text copied to clipboard!');
                    })
                    .catch(err => {
                        alert('Failed to copy text: ' + err);
                    });
            }
        });

        // Download converted text
        downloadButton.addEventListener('click', () => {
            const element = document.createElement('a');
            const fileType = 'text/plain';
            const fileContent = outputText.value;
            const blob = new Blob([fileContent], { type: fileType });
            element.href = URL.createObjectURL(blob);
            element.download = 'converted_text.txt';
            document.body.appendChild(element);
            element.click();
            document.body.removeChild(element);
        });

        // Clear input and output
        clearButton.addEventListener('click', () => {
            inputText.value = '';
            outputText.value = '';
            preview.innerHTML = '';
            preview.style.display = 'none';
            undoStack = [''];
            redoStack = [];
            inputText.focus();
        });

        // Dark mode toggle
        darkModeToggle.addEventListener('click', () => {
            document.body.classList.toggle('dark-mode');
            // Save dark mode preference
            const isDarkMode = document.body.classList.contains('dark-mode');
            localStorage.setItem('darkMode', isDarkMode);
        });

        // Load dark mode preference
        const savedDarkMode = localStorage.getItem('darkMode');
        if (savedDarkMode === 'true') {
            document.body.classList.add('dark-mode');
        }

        // Help modal
        helpButton.addEventListener('click', () => {
            helpModal.style.display = 'block';
        });
        closeHelp.addEventListener('click', () => {
            helpModal.style.display = 'none';
        });
        window.addEventListener('click', (event) => {
            if (event.target == helpModal) {
                helpModal.style.display = 'none';
            }
        });

        // Undo functionality
        undoButton.addEventListener('click', () => {
            if (undoStack.length > 1) {
                redoStack.push(undoStack.pop());
                inputText.value = undoStack[undoStack.length - 1];
                convertText();
            }
        });

        // Redo functionality
        redoButton.addEventListener('click', () => {
            if (redoStack.length > 0) {
                const redoValue = redoStack.pop();
                undoStack.push(redoValue);
                inputText.value = redoValue;
                convertText();
            }
        });

        // Initialize copy as rich text checkbox
        copyAsRichText.checked = false;

        // Initial conversion
        convertText();
    });
</script>
