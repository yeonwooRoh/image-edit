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
        # canvas 생성
    canvas = Canvas(window, width=width, height=height)
    paper = PhotoImage(width=width, height=height)
    # 이미지의 폭을 절반의 값과 높이의 절반의 값의 위치에 이미지를 생성한다.
    canvas.create_image((width / 2, height / 2), image=paper)

    rgb_string = ''
    rgb_image = img.convert("RGB")
    cnt = 0
    # 높이와 너비만큼 더블루프 돌면서 rgb 값을 getpixel() 로 추출하여 16진수 형태로 rgb_string 에 누적시키고 있다.
    for i in range(0, height):
        tmp_string = ""
        for j in range(0, width):
            # 복사된 이미지 객체에 getpixel() 를 이용하여 rgb값을 얻어낼 수 있다.
            r, g, b = rgb_image.getpixel((j, i))
            tmp_string += "#%02x%02x%02x " % (r, g, b)  # x 값 뒤에 한 칸을 공백으로 두어야한다.
            cnt += 1
        rgb_string += "{" + tmp_string + "} "  # } 뒤에 한칸 공백(중요)
    # print(rgb_string, "cnt: ",cnt)
    # rgb 문자열 값을 paper 에 대입시키면서 papar 에 이미지를 출력시키고 있다.
    paper.put(rgb_string)
    canvas.pack()
