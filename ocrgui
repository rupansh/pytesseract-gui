import easygui
from PIL import Image
import numpy as np
from io import BytesIO
import cv2
import pytesseract

filename = easygui.fileopenbox(msg="Choose your Image", multiple=False)

try:
    image = Image.open(filename).convert('L')
except:
    easygui.msgbox(msg="Are you sure you selected an Image?", ok_button="Close")
    exit()

filter = easygui.choicebox(msg='Pick a filter, Use threshold if unsure', title='Filter Pick', choices=("Threshold", "Median Blur(For noisy backgrounds)"))

if filter == "Threshold":
    image = cv2.adaptiveThreshold(np.array(image), 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY,11,2)
elif filter == "Median Blur(For noisy backgrounds)":
    image = cv2.medianBlur(np.array(image), 3)

text = pytesseract.image_to_string(image)

tosave = easygui.filesavebox(msg="Choose the file to save", filetypes=['*.txt'])

textf = open(tosave, 'w')
textf.write(text)

easygui.msgbox(msg=f"Saved text to {tosave}. thanks for using ocrgui!", title='Done', ok_button="Finish")
