# scientific-computing
clc
clear
N = 5000;
    l = 10;
    alpha = [];
    h = 1/N;
    alpha(1) = -(2 + l * l * h*h);
     g = [];
     
    f = h^2 .* ones(N,1);
    f(1) = h^2 - 1;
    g(1) = f(1);
    c = ones(N,1);
    c(N,1) = 0;
    
    b = ones(N,1);
    b(1) = 0;
    a = -(2 + l * l * h*h)*ones(N,1);
 
    
    
    u = ones(N,1);
     
    x = 0:h:1-h;
    
    for i  = 2:N
        alpha(i) = a(i) - ( b(i) / alpha(i-1) )*c(i-1);
        g(i) = f(i) - (b(i)/alpha(i-1))*g(i-1);
    end
    u(N) = f(N) /alpha(N);
    
    for k = 1:(N-1)
        u(N-k) = (g(N-k) - c(N-k)*u(N-k+1)) / alpha(N-k);
    end
   plot(x,u);
    
