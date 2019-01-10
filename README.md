# Convert-multi-json-file-into-a-single-csv-file

import pandas as pd
import json
import os
import glob

path = '...Fashion Project _ Zhou\\foldername'

for filename in glob.glob(os.path.join(path, '*.json')):
    with open(filename) as f:
        data = json.load(f)
        
    file = pd.DataFrame.from_dict(data)
    
    plen = (len(file['posts']))
    
    mentionlist = []
    for i in range(plen):
        mention = file['posts'][i]['mentions']
        mentionlist.append(mention)
    
    mentionflist = []
    for i in range(plen):
        llen = len(mentionlist[i])
        for ii in range(llen):
            mentionflist.append(mentionlist[i][ii])
    
    ps = pd.Series(mentionflist).to_csv(path = '....Fashion Project _ Zhou\\file.csv', index = False, mode = 'a')
