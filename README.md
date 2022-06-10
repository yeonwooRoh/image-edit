# 미니 프토샵 프로그램

import os
from tkinter import *
from tkinter.filedialog import *
from tkinter.simpledialog import *
from PIL import Image, ImageFilter, ImageEnhance, ImageOps

# 전역변수 선언 및 초기화
window, canvas, paper = None, None, None
photo, photo2 = None, None
oriX, oriY = 0, 0
angle = 0

def display_image(img, width, height):
    global window, canvas, paper, photo, photo2, oriX, oriY, angle

    # 화면 크기 설정
    if width + height <= 1000:
        window.geometry(str(int(width * 1.5)) + 'x' + str(int(height * 1.5)))
    else:
        window.geometry(str(width) + 'x' + str(height))

    # print(str(width)+", "+str(height))
    # 기존에 canvas 에 출력한 그림이 있다면
    if canvas is not None:
        canvas.destroy()  # canvas를 깨끗하게 만든다.
