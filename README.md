import json
import matplotlib.pyplot as plt

map_img = plt.imread('map.png')

save_path = '\Users\Administrator\AppData\Local\TurmoilSteam\turmoil_campaign_save.json'

with open(save_path, 'r') as f:
    save_data = json.load(f)

fig, ax = plt.subplots(figsize=(10, 8))

ax.imshow(map_img, extent=(15, 1180, 150, 1110))

for region, data in save_data['estates'].items():
    color = 'g'
    if data['diamonds']:
        ax.scatter(data['i'], 1200 - data['j'], s=10, c=color)
        ax.text(data['i'] - 5, 1200 - data['j'] + 10, "◆", fontsize=7, color='b')
    if data['played']:
        color = 'r'

    print(region)
    print(data)

    if data['oil']<30000:
        fntSz = 7
    elif data['oil']<45000:
        fntSz = 10
    else:
        fntSz = 13

    ax.scatter(data['i'], 1200 - data['j'], c=color, s=12)
    ax.text(data['i'] + 5, 1200 - data['j'] + 5, '%d' % (data['oil'] / 1000), fontsize=fntSz)

plt.show()
