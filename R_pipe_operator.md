https://www.youtube.com/watch?v=ANMuuq502rE

```
install.packages('gapminder')
library(gapminder)
data('gapminder')
View(gapminder)
summary(gapminder)
```
```
x <- mean(gapminder$gdpPercap)
attatch(gapminder)
median(pop)
```

| Eye Colour  | Hight | Weight | Age |
| --- | --- | --- | --- |
| Blue  | 1.8  | 65 | 32 |
| Brown  | 1.9  | 75 | 52 |
| Blue  | 1.7  | 69 | 38 |
| Brown  | 1.9  | 95 | 42 |

```
Data %>% 
	select(Eye colour,Hight,Weight) %>% 
	filter(Eye colour == 'Blue') %>% 
	mutate(BMI = weight / (hight ^ 2)) %>% 
	summarise(Average BMI = mean(BMI)) 
```

```
gapminder %>%
select(country, lifeExp) %>%
filter(country == 'South Africa' | country == 'India') %>%
group_by(country) %>%
summarise(Average_life = mean(lifeExp))
```
```
df1 <- gapminder %>%
select(country, lifeExp) %>%
filter(country == 'South Africa' | country == 'India')
```
```
t.test(data = df1 , lifeExp ~ country)
```
```
gapminder %>%
filter(gdpPercap < 5000) %>%
ggplot(aes(x=log(gdpPercap),y = lifeExp , col = continent ,size = pop ))+
geom_point(alpha=0.3)+
geom_smooth(method = lm)+
facet_wrap(~continent)

```
