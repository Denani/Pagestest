## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Denani/Pagestest/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```Matlab
toda = '[sqrt((x(1,:)-th(1)).^2+(x(2,:)-th(2)).^2);sqrt((x(1,:)-th(3)).^2+(x(2,:)-th(4)).^2) - sqrt((x(1,:)-th(5)).^2+(x(2,:)-th(6)).^2)]';


% toa = exsensor('toa',1,1);
% tdoa = exsensor('tdoa2',3,1)
% s = addsensor(toa,tdoa)


s = sensormod(toda,[2 0 2 6])
s.th = [0,1000 , -1000,0 , 1000,0]
s.x0 = [1 1]
s.pe = [16 0;0 32];

%%
% figure
% s.plot


fs = 1/(ex1_t(2)-ex1_t(1));
y = sig(ex1_y',fs);

X = zeros(length(ex1_y),2);
P = zeros(length(ex1_y),2,2);
for i=1:length(ex1_y)
    temp = estimate(s,y(i),'thmask',[0 0 0 0 0 0]);
    X(i,:) = temp.x0';
    P(i,:,:) = cov(temp.px0);
end
%%

xhat = sig(ex1_y',fs,[],X, zeros(length(ex1_y),2,2), P)
figure
% hold on
% s.plot
xplot2(xhat)

```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Denani/Pagestest/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
