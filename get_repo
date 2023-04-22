```python

import requests
import pygal
from pygal.style import LightColorizedStyle as LCS, LightenStyle as LS


# 执行API调用并存储响应
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'
r = requests.get(url)  # 获取响应对象
print("Status code: ", r.status_code) # 打印状态码，200表示成功

# 将API响应存储在一个变量中
response_dict = r.json()

# 存储有关仓库的信息
repo_dicts = response_dict['items']

# 研究第一个仓库
#repo_dict = repo_dicts[0]
# 获取键的名称
#print("\nKeys:", len(repo_dict))
#for key in sorted(repo_dict.keys()):
#	print(key)

names, plot_dicts = [], []
for repo_dicts in repo_dicts:
    names.append(repo_dicts['name'])
    
    # 定义 '工具提示' pygal提供
    plot_dict = {
        'value': repo_dicts['stargazers_count'],
        'label': repo_dicts['description'], 
        'xlink': repo_dicts['html_url'], 
        }
    plot_dicts.append(plot_dict)

# 可视化
my_style = LS('#336699', base_style=LCS)

# 创建配置对象
my_config = pygal.Config()
my_config.x_label_rotation = 45
my_config.show_legend = False # 隐藏图例
my_config.title_font_size = 24 # 标题
my_config.label_font_size = 14 # 副标题
my_config.major_label_font_size = 18 # 主标签
my_config_truncate_label = 15 # 将项目名缩短为15个字符
my_config.show_y_guides = False # 隐藏图表的水平线
my_config.width = 1000 # 自定义宽度

chart = pygal.Bar(my_config, style=my_style)
chart.title = 'Most-Starred Python Projects on Github'
chart.x_labels = names

chart.add('', plot_dicts)
chart.render_to_file('python_repos.svg')

```
