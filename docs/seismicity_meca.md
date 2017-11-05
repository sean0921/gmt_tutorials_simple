
### 目錄
1. [總覽](/index.md)
2. [GMT介紹及安裝](/intro_install.md)
3. [網路資源及配套軟體](/net_software.md)
4. [第零章: 基本概念及默認值](/basic_defaults.md)
5. [第一章: 製作地圖(地理投影法)](/projection.md)
6. [第二章: XY散佈圖(其他投影法)](/xy_figure.md)
7. [第三章: 等高線圖及剖面](/contour_profile.md)
8. [第四章: 地形圖與色階](/topographic_cpt.md)
9. [第五章: 地震活動性與機制解](/seismicity_meca.md)

---

## 9. 地震活動性與機制解

## 9.1 目的

## 9.2 學習的指令與概念

## 9.3 地震活動性

使用的資料檔:
- [2017地震活動性](dat/2017_catalog.gmt)

成果圖
<p align="center">
  <img src="fig/9_3_seismicity_1.png"/>
</p>

批次檔
```bash
set ps=9_3_seismicity.ps
set data=D:\GMT_data\
set cpt=seis.cpt

# 1. seismicity basemap
gmt gmtinfo 2017_catalog.gmt -i2 -T20 > tmp
set /p cr=<tmp
gmt makecpt -C%cpt% %cr% > tmp.cpt
gmt psbasemap -R119/123/21/26 -JM15 -BwESn -Bxa -Bya -P -K > %ps%
gmt pscoast -R -JM -Df -W1 -S203/211/235 -G230 -P -K -O >> %ps%
awk "{print $1,$2,$3,exp($4)*0.002}" 2017_catalog.gmt | ^
gmt psxy -R -JM -Ctmp.cpt -Sc -K -O >> %ps%

# 2. magnitude calculation
echo 1 > tmp
for /l %%i in (2, 1, 6) do (echo %%i >> tmp)
setlocal ENABLEDELAYEDEXPANSION
set vidx=0
for /f %%i in ('awk "{print exp($1)*0.002}" tmp') do (
    set /A vidx=!vidx! + 1
    set var!vidx!=%%i
)
set var

# 3. legend set
echo H 18 1 Legend > tmp
echo D 0.4 1p >> tmp
echo G .7 >> tmp
echo B tmp.cpt 0.2 0.3+ml -Ba40f20+l"Depth (km)" >> tmp
echo G .3 >> tmp
echo M 121 23.5 100+u +f >> tmp
echo G .1 >> tmp
echo D 0.6 1p,0,- >> tmp
echo G .2 >> tmp
echo L 14 0 C Magnitude >> tmp
echo N 3 >> tmp
echo G .2 >> tmp
echo S .5 c %var1% 0 0 1 1 >> tmp
echo S .5 c %var2% 0 0 1 2 >> tmp
echo S .5 c %var3% 0 0 1 3 >> tmp
echo G .4 >> tmp
echo S .5 c %var4% 0 0 1 4 >> tmp
echo S .5 c %var5% 0 0 1 5 >> tmp
echo S .5 c %var6% 0 0 1 6 >> tmp
echo G .3 >> tmp
gmt pslegend tmp -R -JM -C.1/.1 -Dx.1/14+w5 -F+g245+p1+s4p/-4p/gray50 ^
--FONT_ANNOT_PRIMARY=10p --FONT_LABEL=14p -K -O >> %ps%

gmt psxy -R -JM -T -O >> %ps%
gmt psconvert %ps% -Tg -A -P
del tmp
```

## 9.4 

## 9.5 

## 9.6 習題

## 9.7 參考批次檔
列出本章節使用的批次檔，供讀者參考使用，檔案路經可能會有些許不同，再自行修改。


---

[上一章](/topography_cpt.md) -- [下一章](/seismicity_histo.md)