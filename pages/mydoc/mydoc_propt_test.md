---
title: PROPT test
keywords: PROPT, matlab
last_updated: July 12, 2018
tags: [getting_started]
summary: "PROPT test to see how it can be implemented into github pages"
sidebar: mydoc_sidebar
permalink: mydoc_propt_test.html
folder: mydoc
---

Find u over t in [0;t_F] to minimize

$J=t_F$

And so on

#### Matlab code
'''matlab
%% Problem setup
toms t
toms t_f
p = tomPhase('p', t, 0, t_f, 30);
setPhase(p);
tomStates x1 x2
tomControls u
% Initial guess
% Note: The guess for t_f must appear in the list before expression involving t.
x0 = {t_f == 20
icollocate({x1 == 300*t/t_f; x2 == 0})
collocate(u==1-2*t/t_f)};
% Box constraints
cbox = {10 <= t_f <= 40
-2 <= collocate(u) <= 1};
% Boundary constraints
cbnd = {initial({x1 == 0; x2 == 0})
final({x1 == 300; x2 == 0})};
% ODEs and path constraints
ceq = collocate({dot(x1) == x2; dot(x2) == u});
% Objective
objective = t_f;

%% Solve the problem
options = struct;
options.name = 'Bang-Bang Free Time';
options.prilev = 1;
solution = ezsolve(objective, {cbox, cbnd, ceq}, x0, options);
t  = subs(collocate(t),solution);
x1 = subs(collocate(x1),solution);
x2 = subs(collocate(x2),solution);
u  = subs(collocate(u),solution);

%% Plot the solution
subplot(2,1,1)
plot(t,x1,'*-',t,x2,'*-');
legend('x1','x2');
title('Bang-Bang Free Time state variables');
subplot(2,1,2)
plot(t,u,'+-');
legend('u');
title('Bang-Bang Free Time control');
'''

#### Output
'''matlab
Run tomlablic to display license information
Done with setting TOMLAB paths
Problem type appears to be: lpcon
Time for symbolic processing: 1.1829 seconds
Starting numeric solver
===== * * * =================================================================== * * *
TOMLAB - Linkoping University Ac. department  705016. Valid to 2100-01-01
=====================================================================================
Problem: ---  1: Bang-Bang Free Time            f_k      30.019823270451944097
                                       sum(|constr|)      0.000028878808460443
                              f(x_k) + sum(|constr|)     30.019852149260405128
                                              f(x_0)     20.000000000000000000

Solver: snopt.  EXIT=0.  INFORM=1.
SNOPT 7.2-5 NLP code
Optimality conditions satisfied

FuncEv    1 ConstrEv  526 ConJacEv  526 Iter  136 MinorIter  185
CPU time: 0.740000 sec. Elapsed time: 1.280843 sec.
'''
