# coding: utf-8

import pandas as pd
import csv
import re

input = pd.DataFrame(columns = ('GRANTEE','OWNER','TABLE_NAME','GRANTOR','PRIVILEGE','GRA','HIE'))
cols = ['GRANTEE','OWNER','TABLE_NAME','GRANTOR','PRIVILEGE','GRA','HIE']

skippercount = 6 #for skipping duplicate of header labels.
columncount = 0
indcnt = 0

newrow = []

txtfile = 'table.txt'
print "open text file.."
with open(txtfile, 'rb') as inputfile:
    print "Extract and Transform file"
    for line in inputfile:
        """
        CLEAN DATA OF HEADER ROWS, SPACES AND SEPERATE EACH WORD INTO A TOKEN
        """

        if line[:7] == "GRANTEE" or skippercount < 6:
            skippercount -= 1
            if skippercount == 0:
                skippercount = 6
            continue #skip this line in file
       #process line of text for data extraction.
        newline = re.sub('\s+',' ',line)
        newline =  newline.strip()
        tokens = newline.split(" ")
        #additional processing, this shot out errors for some lines:
        try:
            tokens.remove('\n')
        except:
            pass
        try:
            tokens.remove('\t')
        except:
            pass
        try:
            tokens.remove('\r')
        except:
            pass
        """
        For every 7 tokens, make a new row in data frame, delete temporary list and repeat
        """

        for value in tokens:
            if len(value)>1 and value != '':
                newrow.append(value)
                if columncount == 6:
                    input.loc[indcnt] = newrow #add new row to dataframe.
                    indcnt +=1
                    newrow = []
                    columncount = 0
                else:  
                    columncount +=1
            else:
                continue
print "Done! now printing to csv :)"
input.to_csv('fixed_table.csv',sep=',')
