# Plotting cơ bản với pandas
Pandas có các chức năng được tích hợp có thể được gọi trên Chuỗi hoặc DataFrame. Chúng sử dụng các mặc định thông minh hợp lý và nhanh chóng đưa ra ý tưởng về những gì đang diễn ra. Tuy nhiên trước khi tạo biểu đồ cần phải thiết lập và cài đặt thư viện. 
import pandas as pd
import numpy as np
Và tải dữ liệu về notebook cũng như khám phá chuyển đổi gán nhãn để đối với các nước có thu nhập đầu người theo phân loại (thấp nhất, thấp, trung bình, cao nhất). Dữ liệu được sử dụng là dữ liệu về chỉ số hạnh phúc của thế giới được gộp qua các năm từ năm 2007 đến năm 2018

## Load the data
data = pd.read_csv('https://raw.githubusercontent.com/FBosler/AdvancedPlotting/master/combined_set.csv')# this assigns labels per year
data['Mean Log GDP per capita']  = data.groupby('Year')['Log GDP per capita'].transform(
    pd.qcut,
    q=5,
    labels=(['Lowest','Low','Medium','High','Highest'])
)

### Để tạo một biểu đồ, hãy gọi .plot (kind = <TYPE OF PLOT>) trên dữ liệu của bạn, như sau:
np.exp(data[data['Year']==2018]['Log GDP per capita']).plot(
kind='hist'
)
 
 ![2018: Một số nhóm các nước có bình quần thu nhập theo đầu người. Không ngạc nhiên vì hầu hết các nước nghèo có bình quân đầu người thấp](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download.png?raw=true)
 
2018: Một số nhóm các nước có bình quần thu nhập theo đầu người. Không ngạc nhiên vì hầu hết các nước nghèo có bình quân đầu người thấp.

### Có năm thông số chính sử dụng khi vẽ với Pandas:
kind: Pandas phải biết loại biểu đồ nào bạn muốn tạo, các lựa chọn sau là có sẵn, hist, bar, barh, scatter, area, kde, line, box, hexbin, pie.
figsize: Cho phép ghi đè kích thước đầu ra mặc định rộng 6 inch và cao 4 inch. figsize mong đợi một bộ giá trị (ví dụ: figsize = (12,8))
title: Thêm tiêu đề vào biểu đồ.
bins: Cho phép ghi đè chiều rộng các bins cho biểu đồ. bins mong đợi một danh sách hoặc chuỗi giá trị giống như danh sách (ví dụ: bins = np.arange (2,8,0.25))
xlim / ylim: Cho phép ghi đè các giá trị mặc định cho các giá trị lớn nhất và nhỏ nhất của trục. Cả hai, xlim và ylim đều mong đợi một bộ giá trị (ví dụ: xlim = (0,5))
Hãy cùng đi đến các loại khác của biểu đồ

## Vertical bar chart (biểu đồ cột dọc)
data[
data['Year'] == 2018
].set_index('Country name')['Life Ladder'].nlargest(15).plot(
kind='bar',
figsize=(12,8)
)
 
![2015: Danh sách 15 nước có chỉ số hạnh phúc cao nhất trong đó dẫn đầu là Na Uy](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(1).png?raw=true)
  
2015: Danh sách 15 nước có chỉ số hạnh phúc cao nhất trong đó dẫn đầu là Na Uy

## Horizontal bar chart (biểu đồ cột ngang)
np.exp(data[
data['Year'] == 2015
].groupby('Continent')['Log GDP per capita']\
.mean()).sort_values().plot(
kind='barh',
figsize=(12,8)
)
 ![2018: Trung bình GDP đầu người theo các lục địa được dẫn đầu bởi Australia và New Zealand ](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(2).png?raw=true)
2018: Trung bình GDP đầu người theo các lục địa được dẫn đầu bởi Australia và New Zealand 

## Box plot
data['Life Ladder'].plot(
kind='box',
figsize=(12,8)
)
  ![Biểu đồ hộp về sự phân bố của Life Ladder cho thấy giá trị trung bình nằm ở đâu đó khoảng 5.5, từ các giá trị dưới 3 đến 8.](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(3).png?raw=true)
Biểu đồ hộp về sự phân bố của Life Ladder cho thấy giá trị trung bình nằm ở đâu đó khoảng 5.5, từ các giá trị dưới 3 đến 8.

## Scatter plot
data[['Healthy life expectancy at birth','Gapminder Life Expectancy']].plot(
    kind='scatter',
    x='Healthy life expectancy at birth',
    y='Gapminder Life Expectancy',
    figsize=(12,8)
)

  ![Biểu đồ phân tán của Báo cáo hạnh phúc của thế giới Healthy life expectancy khi sinh so với Gapminder Life Expectancy cho thấy mối tương quan cao giữa hai yếu tố này (dự kiến)](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(4).png?raw=true)
Biểu đồ phân tán của Báo cáo hạnh phúc của thế giới Healthy life expectancy khi sinh so với Gapminder Life Expectancy cho thấy mối tương quan cao giữa hai yếu tố này (dự kiến)

## Hexbin chart
data[data['Year'] == 2018].plot(
kind='hexbin',
x='Healthy life expectancy at birth',
y='Generosity',
C='Life Ladder',
gridsize=20,
figsize=(12,8),
cmap="Blues", # defaults to greenish
sharex=False # required to get rid of a bug
)
  ![2018: Biểu đồ Hexbin, Biểu đồ tuổi thọ chống lại Generosity. Màu sắc của các bin cho biết tuổi thọ trung bình của bậc thang trong bin tương ứng.](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(5).png?raw=true)
2018: Biểu đồ Hexbin, Biểu đồ tuổi thọ chống lại Generosity. Màu sắc của các bin cho biết tuổi thọ trung bình của bậc thang trong bin tương ứng.

## Pie chart
data[data['Year'] == 2018].groupby(
['Continent']
)['Gapminder Population'].sum().plot(
kind='pie',
figsize=(12,8),
cmap="Blues_r", # defaults to orangish
)

  ![2018: Biểu đồ hình tròn hiển thị tổng dân số theo châu lục.](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(6).png?raw=true)
2018: Biểu đồ hình tròn hiển thị tổng dân số theo châu lục

## Stacked area chart

data.groupby(
['Year','Continent']
)['Gapminder Population'].sum().unstack().plot(
kind='area',
figsize=(12,8),
cmap="Blues", # defaults to orangish
)
  ![Dân số trên toàn cầu đang gia tăng.](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(7).png?raw=true)
2018: Biểu đồ hình tròn hiển thị tổng dân số theo châu lục
Dân số trên toàn cầu đang gia tăng.

## Line chart
data[
data['Country name'] == 'Germany'
].set_index('Year')['Life Ladder'].plot(
kind='line',
figsize=(12,8)
)
 ![Biểu đồ đường mô tả sự phát triển của hạnh phúc ở Đức.](https://github.com/ngohaily/Visualization/blob/gh-pages/images/download%20(8).png?raw=true)
Biểu đồ đường mô tả sự phát triển của hạnh phúc ở Đức.

# Tóm lại
Tạo biểu đồ với Pandas rất tiện lợi. Nó có thể dễ dàng truy cập và nhanh chóng. Tuy nhiên nó khá không được đẹp và chỉ ứng dụng với các biểu đồ đơn giản và cơ bản nhất. 
