clc

clear all

format short

A = \[1 3; 1 1; 1 -1\];

B = \[10; 6; 2\];

y1 = 0:1:max(B);

x11 = (B(1) - A(1,1).\*y1) ./ A(1,2);

x21 = (B(2) - A(2,1).\*y1) ./ A(2,2);

x31 = (B(3) - A(3,1).\*y1) ./ A(3,2);

x11 = max(0,x11);

x21 = max(0,x21);

x31 = max(0,x31);

plot(y1,x11,'r',y1,x21,'b',y1,x31,'g')

grid on

title('Graphical Method')

xlabel('x1')

ylabel('x2')

legend('x1 + 3x2 = 10','x1 + x2 = 6','x1 - x2 = 2')

cx1 = find(y1 == 0);

c1 = find(x11 == 0);

Line1 = \[y1(:,\[c1 cx1\]); x11(:,\[c1 cx1\])\]';

c2 = find(x21 == 0);

Line2 = \[y1(:,\[c2 cx1\]); x21(:,\[c2 cx1\])\]';

c3 = find(x31 == 0);

Line3 = \[y1(:,\[c3 cx1\]); x31(:,\[c3 cx1\])\]';

corpt = unique(\[Line1; Line2; Line3\],'rows');

pt = \[\];

for i = 1:size(A,1) 

    for j = i+1:size(A,1)

        X = \[A(i,:); A(j,:)\] \\ \[B(i); B(j)\];

        pt = \[pt; X'\];

    end

end

allpt = unique(\[pt; corpt\],'rows');

P = \[\];

for i = 1:size(allpt,1)

    x1 = allpt(i,1);

    x2 = allpt(i,2);

    if x1 + 3\*x2 &lt;= 10 && x1 + x2 &lt;= 6 && x1 - x2 &lt;= 2 && x1 &gt;= 0 && x2 &gt;= 0

        P = \[P; x1 x2\];

    end

end

P = unique(P,'rows')

c = \[1 5\];

fn = zeros(size(P,1),1);

for i = 1:size(P,1)

    fn(i) = sum(P(i,:).\*c);

end

ver_fns = \[P fn\]

\[Optval,optposition\] = max(fn);

Opt_Point = ver_fns(optposition,:)

OPTIMAL_BFS = array2table(Opt_Point,'VariableNames',{'x1','x2','Z'})

hold on

plot(P(:,1), P(:,2), 'ko', 'MarkerSize',8, 'MarkerFaceColor','y')

plot(Opt_Point(1), Opt_Point(2), 'r\*', 'MarkerSize',12)

legend('x1 + 3x2 = 10','x1 + x2 = 6','x1 - x2 = 2','Feasible Points','Optimal Point')

hold off

---

format short

clear all

clc

C = \[3 -5 0 0\];

A = \[1 1 1 0;  -2 1 0 1\];

b = \[6;-9\];

m = size(A,1);

n = size(A,2);

nv = nchoosek(n,m);

t = nchoosek(1:n,m);

sol = \[\];

if n&gt;=m

for i = 1:nv

    y = zeros(n,1);

    x = A(:,t(i,:))\\b;

    if all (x&gt;=0 & x\~=inf & x\~=-inf)

        y(t(i,:)) = x;

        sol = \[sol y\];

    end

end

else

    error('Equation is larger than variable')

end

Z = C\*sol

\[Zmin, Zind\] = min(Z)

BFS = sol(:,Zind)

optval = \[BFS' Zmin\]

OPTIMAL_BFS = array2table(optval)

OPTIMAL\_[BFS.Properties](http://BFS.Properties).VariableNames = {'x_1', 'x_2', 'x_3', 'x_4', 'Value_of_Z' }
