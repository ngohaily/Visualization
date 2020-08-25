# Plotting with geopandas
Nếu chúng ta đã biết plotting các biểu đồ với pandas thì với thư viện geopandas chúng ta có thể plotting với dữ liệu không gian. Tuy nhiên trước khi thực hiện các việc này thì cần phải import thư viện vào notebook
import geopandas as gpd
import matplotlib.pyplot as plt
## Load data
Hiện nay việc làm việc trên cloud là rất phổ biến chúng ta có thể không cần thiết phải tải file dữ liệu về máy mà có thể điều hướng trực tiếp về kho dữ liệu trên cloud

url = "https://data.vietnam.opendevelopmentmekong.net/en/dataset/100d98c8-4ffc-4b5b-b2a5-c6b71d2eff66/resource/c8b14875-6ab9-4a3e-99e9-8352f695cd77/download/covid-19-provinces.geojson"
df = gpd.read_file(url)
# Plotting thuộc tính của file dữ liệu
df.head()
![hien thi thuoc tinh file]https://github.com/sigvn/Visualization/blob/gh-pages/images/attribute.png

## Plotting graphic
df.plot()
![vn] https://github.com/sigvn/Visualization/blob/gh-pages/images/vn.png

## Xác định biến và khoảng giá trị để hiển thị
variable=df.infected
vmin,vmax = 0,372
df.plot(column=variable)
![vn1]https://github.com/sigvn/Visualization/blob/gh-pages/images/vn1.png
## Tạo legend đánh giá với độ chính xác của legend
import matplotlib.pyplot as plt
fig, ax = plt.subplots(1, figsize=(10,10))
df.plot(column= variable,ax=ax, legend=True)

![vn3]https://github.com/sigvn/Visualization/blob/gh-pages/images/vn3.png
