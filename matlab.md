# Welcome to My MATLAB Work Page

Most of the work I had to do with MATLAB solely focused on analytical problems and physics problems, such as plotting an object being thrown at sea level with or without air density with different launching angles. I worked with quadratic motion with friction, and worked with the Saha Equation in astrophysics. There were many other examples, since I had to use MATLAB for almost every class. More will be added at a later time.


### Geometric Series

function geometricseries
%Sums the geometric series a^0 + a^1 + a^2 + ... + a^n for n = 0 to N
%  and plots versus N to determine convergence.  If it is a convergent
%  series, the value of convergence (for N = infinity) is also plotted on
%  the graph.
close all; clc;

a =-0.95; N = 100;
SUM = zeros(1,N+1);
for i = 0:N;
    for j = 0:i;
     SUM(i+1) = SUM(i+1) + a^j;
    end
end
plot(0:N,SUM,'-k','LineWidth',2);
xlabel('N','FontSize',16); ylabel('Sum','FontSize',16);
title(['\Sigma_{n=0}^N (',num2str(a,'%.3f'),')^{n}'],'FontSize',16);
hold on
if abs(a)>=1;
    axis([0 N -1.5*SUM(N+1) 1.5*SUM(N+1)]);
    legend('Divergent series','Location','Best');    
else
    plot(0:N/100:N,1/(1-a)*ones(1,101),'--r','LineWidth',2);
    axis([0 N -1.5*1/(1-a) 1.5*1/(1-a)]);    
    legend('Sum','Limit of convergence','Location','Best');
end
end

### Taylor Expansion

function taylorexpand
%Plots a single variable function and the first N terms of its Taylor
%expansion about a point x0 within the interval xi to xf.
close all; clc; syms x;
F = x.*exp(x)*cos(x); 
%Define the function
xi = -2; xf = 2; 
%Set the interval
x0 = 0; 
%Set the expansion point (somewhere in the plotting interval).
%It must have a non-zero slope at this point, or you will get an error.
N = 3;  
%Plot the first N terms.  Must be greater than 1.
xstep = (xf - xi)/100;  
%Set the x step
T = taylor(F,x,'ExpansionPoint',x0,'Order',N);   
%Take the taylor expansion
xgrid = xi:xstep:xf;    
%Set the x grid
f = matlabFunction(F);  
%Convert from symbolic to a function
t = matlabFunction(T);
plot(xgrid,f(xgrid),'k','LineWidth',2)  
%Plot the function
hold on
plot(xgrid,t(xgrid),'--r','LineWidth',2);  
%Plot the Taylor expansion
xlabel('x','FontSize',12); ylabel('y','FontSize',12);
title('Function and its Taylor Expansion','FontSize',14);
legend('Function','Taylor expansion','Location','best')
F=char(F);T=char(T);     
%Display the function and its Taylor expansion.
fprintf('Function = %s \nTaylor series = %s\n',F,T);
end



### Temperature

%Finding the constants C and S by using a first-order ploynomial from 
%The given equation u = (C*T^(3/2)) / (T + S) and will be displayed in
%command window.
%The given values are the temperature(Celsius) and viscosity (property of
%gases and fluids) and are typed in below. 
%The first plot is the equation T^(3/2)/u = (1/C)*T + S/C (y) Vs. Temp.(x)
%Second plot will be Temp in Celsius(x) Vs. viscosity(U) 
 
T = [-20, 0, 40, 100, 200, 300, 400, 500, 1000];
%Temperature, Celsius
K = T + 273;
%Temperature, converting to Kelvin
u = [1.63, 1.71, 1.87, 2.17, 2.53, 2.98, 3.32, 3.64, 5.04];
%Viscosity, units in Ns/m^2; 
U = 10^(-5) .* u;
%The new viscosity (U) has been multiplied by *10^-5
 
C = K(:)\U(:)               %First constant
S = K(:)\U(:)               %Second constant
Tu = (1./C).* K(:) + S./C;  %Solve for T^(3/2)/u
 
figure(1);
plot(K, Tu,'r');
xlabel('Temperature(Kelvin)');
ylabel('T^(3/2) /u');
%Plot one where its Temp. vs Tu (T^(3/2)/u = (1/C)*T + S/C)
 
figure(2);
plot(T, U, 'b');
% The x-axis (T) is directly from the given variables that were given
%in Celsius.
xlabel('Temperature(Celsius)');
ylabel('Viscosity(Ns/m^2)');
%Plot two where Temp. vs u(viscosity)
