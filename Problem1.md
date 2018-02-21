# scientific-computing
clc
clear
N = 1000;
    l = 10; %lamda
    a = [];
    h = 1/N; %h has 'N' equally spaced intervals
    a(1) = -(2 + l * l * h*h);
     g = [];
     
    f = h^2 .* ones(N,1);
    f(1) = h^2 - 1;
    g(1) = f(1);
    c = ones(N,1);
    c(N,1) = 0;
    
    b = ones(N,1);
    b(1) = 0;
    a = -(2 + l * l * h*h)*ones(N,1);
 
    
    
    u = ones(N,1); %u has N number of rows and one column
     
    x = 0:h:1-h; 
    
    for i  = 2:N 
        a(i) = a(i) - ( b(i) / a(i-1) )*c(i-1);
        g(i) = f(i) - (b(i)/a(i-1))*g(i-1);
    end
    u(N) = f(N) /a(N);
    
    for k = 1:(N-1)
        u(N-k) = (g(N-k) - c(N-k)*u(N-k+1)) / a(N-k);
    end
    %given exact function for comparison
    y=((sinh(k-k*x) + sinh(k*x))/sinh(k)-1)*(1/k^2) + (sinh(k-k*x))/sinh(k); 

   plot(x,u,'o',x,y,'*');
   legend('approximate', 'exact');
