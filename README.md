# Wave-Equation-Instruments
Generating classical guitar sounds and more using the wave equation, modeled by partial derivatives.
To learn about the project's details, please read the paper attached WaveEq.pdf.

Introduction
The wave equation, shown below in equation 1, is a second-order linear partial differential equation which describes the behavior and properties of waves.
∂2u = c2 ∂2u (1) ∂t2 ∂x2
To understand the wave equation, we must first understand the components of the one-dimensional wave equation. c represents the speed of the wave. Therefore, if we are studying an electromagnetic wave, c would always equal the speed of light. t represents time.
u equals the displacement of the wave along the y axis, while x represents
the spatial distribution of the wave along the x axis. 2 Deriving the Wave Equation

The three main assumptions one must make when deriving the wave equation are:
1. Gravity is negligible compared to the tension in the string
2. Tension is constant across all x locations throughout the string.
3. If we were to take a small zoomed-in sample of the wave, from x to δx, deflections would be small (This means each point in the string can ONLY move vertically)

Derivation
We look at an infinitesimally-small piece of the string, ∆x.
We only consider the vertical forces: Substituting m = ρ∆x, where ρ is linear density
Fy = may = ρ(∆x)(utt)
From summing the vertical forces:
Fy = F2 − F1
= FT sin(θ2) − FT sin(θ1)
From our assumption of small deflections, or small angles of θ, we can substitute in sin(θ) = tan(θ):
Fy = FT [tan(θ2) − tan(θ1)]
Since tan(θ) is equal to the slope of the wave function in the x-y (interchangeably the x-u) plane,
Fy = may
we can say that
Fy =FT
Substituting Fy = ρ(∆x)(utt) and x2 = x1 + ∆x, and changing our notation x1 to x since we can
look at any location of x,
FT􏰂∂u ∂u 􏰃 utt=ρ∆x ∂x(x+∆x,t)−∂x(x,t)
Since we are assuming ∆x to be infinitesimally small, we take the limit:
tan(θ) = ∂u ∂x
and
􏰂∂u ∂u 􏰃 ∂x(x2,t)−∂x(x1,t)
 Because we know FT ρ
ρ
equals c2, we get the wave equation:
utt = lim
∂x
(x,t)
FT􏰂∂u ∆x→0ρ∆x ∂x
(x+∆x,t)−
∂u 􏰃
 FT 1􏰂∂u ∂u􏰃 = lim (x+∆x,t)− (x,t)
ρ ∆x→0 ∆x ∂x ∂x = FT uxx
utt = c2uxx
2

Solutions of the Wave Equation
To solve partial differential equations, one must specify boundary conditions to arrive at unique solutions. For our purposes, the function (our string) is fixed at x = 0 and x = L, where L is the length of our string. So, our boundary conditions are:
u(0,t) = 0 and u(L,t) = 0

We will not explain the method of solving the wave equation because it is outside the scope of the
contents of the first semester of Multivariable Calculus, but one form of the solution is
u(x, t) = A sin(x − ct) + B sin(x + ct) (2)
where A and B are constant that result in u(x,t) meeting the boundary conditions. This solution represents the sum of two moving waves, both with speed c, one moving to the left and one moving to the right. It is a standing wave.
Figure 3: The red and blue moving waves sum to form the black standing wave
This solution looks too simple to represent a real guitar string, but it is the basic building block of the real model.
We introduce the superposition principle: the principle is a property of solutions to linear par- tial differential equations. First, let’s define linear partial differential equations.
A linear partial differential equation is called ”linear” because terms containing the unknown functions are only first order (raised to the power of 1). For example, a linear PDE can take the form:
a ∂f +a ∂f +...+a ∂f =g(x,y) 1 ∂x 2 ∂y n ∂n

where f is the unknown function, g is a known function, and a1,a2,...,an are the coefficients of the terms.
The superposition principle states that if f1 and f2 are two solutions to a linear partial differ- ential equation, then the sum f1 + f2 is also a solution to the equation. In other words, the superposition principle allows us to construct new solutions to a linear partial differential equation by adding together known solutions.
Here is an example demonstrating why the principle works: consider the linear partial differential equation
∂f =a∂2f +b∂2f ∂t ∂x2 ∂y2

where a and b are constants.
Suppose that we have two solutions to this equation, f1 and f2, which are defined on the same domain and satisfy the boundary conditions of the problem. Then the sum f1 +f2 is also a solution to the equation, because it satisfies the equation itself:
∂(f1 +f2) = ∂f1 + ∂f2 ∂t ∂t ∂t
=a∂2f1 +b∂2f1 +a∂2f2 +b∂2f2 ∂x2 ∂y2 ∂x2 ∂y2
= a∂2(f1 + f2) + b∂2(f1 + f2) ∂x2 ∂y2
Since the wave equation is linear, we can use the superposition principle to better understand the solution: the sum of any number of solutions in the form of equation 2 is also a solution. This means that we can add infinitely many of them to construct complex models for real-world situations.
An interesting fact: the Fourier Series, which represents periodic functions as the sum of a se- ries of sines and cosines, can be used to solve the wave equation, by expressing the solution as a series of sines and cosines.

The True Wave Equation
The true wave equation given below, shares many properties with the one-dimensional wave equa- tion. This is the equation we will use to generate unique audio sounds.
∂2y − 1 ∂2y − γ ∂y − l2 ∂4y = 0 (3) ∂x2 c2 ∂t2 ∂t ∂x4

An immediate difference is the addition in constants. These additional constants are γ, c, and l. These correspond to the damping constant (units: s/m), the speed of the wave (m/s), and the characteristic length (stiffness constant) of the wave respectively. These additions in constants allow the audio generated to be more realistic. Thus, by plugging in different constants, we can generate sounds with different tonalities even if they share the same frequencies. The characteristic sound of a wounded-steel string of the classical guitar has units of 5e−5 for γ and the stiffness. c equals two times the characteristic length multiplied by frequency.
To use python to solve the true wave equation for each period of time to generate audio, one uses the discrete form of the true wave equation.
ym −2ym +ym 1 ym+1 −2ym +ym−1 ym+1 −ym−1 j+1jj−1−j jj−γj j ∆x2 c2 ∆t2 ym −4ym +4ym −4ym 2∆t +ym −l2 j−2 j−1 j j+1 ∆x4 j+2 =0 Using this equation we can find the next instantaneous value. Given by:
 m+1􏰂1γ􏰃−1􏰂1􏰀m mm􏰁1􏰀m−1m􏰁γm−1 yj = c2∆t2 + 2∆t ∆x2 yj+1 −2yj +yj−1 − c2∆t2 yj −2yj + 2∆tyj
   l2 􏰃(5) − 􏰀ym − 4ym + 6ym − 4ym + ym 􏰁
∆x4 j−2 j−1 j j+1 j+2

This equation generates the audio by plugging in the values of the two previous amplitudes. For
 the first time one applies the function, the given initial value is plugged in for both ym−1 and ym. jj
Python and other software can be used to generate audio files from initial conditions inputted into equation 5.

Fourier Series
Fourier series are mathematical series that breaks down a function into sin and cos functions. For our case, we use the Fourier series to find the relative amplitudes of harmonic frequencies, in order to generate the sound of a string pluck.
􏰄L 0
Using a fourier series, we can break up our function into the sum of individual amplitudes of the harmonics. We use Python to compute the integral and calculate the amplitude of the wave with the frequency of the harmonic of interest. Adding the sine waves of every harmonic together, we generate the simulated audio of the string pluck.
Amplitude of harmonic n at time t ∝
u(x, t) sin(nπx/L)dx (6)

Applications 
Music
Different values of the wave equation can generate the different sounds audio engineers use to repli-
cate real-life instruments. Because musical instruments produce sound waves, the wave equation
also fundamentally explains how the instruments work. This is done using the component FT ρ
equals c2 from the wave equation. In other words, Tension divided by linear density equals the speed of the wave squared. Linear density equals mass divided by length. Because of the equation:
FT =c2 ρ
We know that the speed of the wave is directly proportional to the frequency, or pitch of the instrument. The higher the strings on this classical guitar, the lower the pitch. First, if one looks at the top three strings, they will notice that the higher the strings, the thicker they are. Because they are all made of the same material, thicker-wound strings have a higher mass, which thus increases the string’s linear density and results in a lower wave speed. Since wave speed is directly propor- tional to frequency(pitch), a lower wave speed produces a lower pitched note.
The bottom three strings are made of a different material: nylon. Since nylon has a lower lin- ear density, a string of the same thickness as the steel strings would still produce a higher pitch. This is why the highest nylon string is of equal thickness to the lowest steel string yet still produces a higher pitch.
