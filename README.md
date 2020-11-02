# 프로젝트명 : 자연어처리 기반의 주가분석 및 예측시스템
- 팀명 : Project_TurnAround
- 멘토 : 정좌연🗽 PE 
- 멘티 : 이지훈👤, 김서정✌, 구병진🎶, 강민재😁, 이문형😎


# 1. Model Structure
- 데이터 수집 모듈 : [app.py](https://github.com/quantylab/rltrader)_정형 데이터,   [app.py](https://github.com/quantylab/rltrader)_비정형 데이터
- 데이터 분석 모듈 : [app.py](https://github.com/quantylab/rltrader)_AutoML, Prophet, NLP,  [app.py](https://github.com/quantylab/rltrader)_강화 학습
- 실행 모듈 : [app.py](https://github.com/quantylab/rltrader)

# 2. Environment Setup
가상환경에서 설치하는 것을 권장함( 가상환경 설치방법 : conda create -n [원하는 가상환경이름] )
- OS : Windows 10 x64
- IDE : PyCharm, Jupyter Notebook, Google Colaboratory
- Language : Python 3.7 (Anaconda 3.7)

# 3. Library Installation
## 1) Data Analysis
```bash
# (1) 행렬 연산
pip install numpy

# (2) 데이터 분석
pip install pandas

# (3) 시각화
pip install matplotlib
pip install seaborn
pip install mplfinance

# (4) 한국의 공휴일
pip install workalender

# (5) 날짜
pip install DateTime
```

## 2) Web Application
(1) streamlit 설치
```bash
pip install streamlit
```

## 3) Financial Data API
(1) Yahoo Finance API 설치
```bash
pip install yfinance --upgrade --no-cache-dir
```

(2) investing.com API 설치
```bash
pip install investpy
```

(3) KRX API 설치
```bash
pip install pykrx
```

(4) ta-lib 설치 - 기술적 분석 (보조지표)
```bash
pip install ta-lib
```
설치에 실패할 경우에는, [link](https://www.lfd.uci.edu/~gohlke/pythonlibs/#ta-lib)에서 버전에 맞는 파일을 다운로드해서 아래와 같이 설치함
- Ex) python 3.7/64비트 버전 사용시
```bash
pip install TA Lib‑0.4.19‑cp37‑cp37m‑win_amd64.whl
```

## 4) Prophet
(1) Prophet 설치
```bash
conda install -c conda-forge fbprophet
pip install pystan
pip install prophet
pip install fbprophet
```

## 5) AutoML
(1) pycaret 설치
```bash
pip install pycaret
```

## 6) Reinforcement Learning
Anaconda 3.7+
(1) TensorFlow 1.15.2 설치
```bash
pip install tensorflow==1.15.2
```

(2) Keras 2.2.4 설치
```bash
pip install Keras=2.2.4
```

## 7) Natural Language Processing
[ReadMe.md](https://github.com/ejihoon6065/Project_TurnAround/blob/master/NLP/ReadMe.md)에서 자세한 설치 방법 확인
<p>
<p align="Left">
    <a href="https://github.com/ejihoon6065/Project_TurnAround/blob/master/NLP/ReadMe.md">  
        <img alt="Contributor Covenant" src="https://img.shields.io/badge/NLP%20-Mecab%20-ff69b4.svg">
    </a>
</p>

```bash
# (1) Konlpy 설치
pip install JPype1‑0.6.3‑cp37‑cp37m‑win_amd64.whl

# (2) Mecab 설치
pip install mecab_python-0.996_ko_0.9.2_msvc-cp37-cp37m-win_amd64.whl
```
# 4. Model Description
## 1) Data Collection Module
data sources : 정형/비정형
data format : 정형/비정형
| Open    | High    | Low     | Close   | Volume     | Labeling | ma_5               | ma_10              | ma_15              | ma_20              | ma_30              | ma_60              | ma_120             | ema_5              | ema_10             | ema_15             | ema_20             | ema_30             | ema_60             | ema_120            | wma_5              | wma_10             | wma_15             | wma_20             | wma_30             | wma_60             | wma_120            | ma_v5        | ma_v10       | ma_v20       | ma_v60            | ma_v120           | ubb                | mbb                | lbb                | macd                 | macdsignal9          | macdhist              | rsi                | slowk              | slowd              | fastk                | fastd              | fastk_rsi           | fastd_rsi               | cci                 | willR                 | sar    | adx                | plus_di            | plus_dm            | atr                | obv           | var                | kospi_inst_volume | kospi_indi_volume | kospi_fore_volume | kospi_etc_volume | kospi_short_sell_volume | kospi_inst_value | kospi_indi_value | kospi_fore_value | kospi_etc_value | kospi_short_sell_value | kospi_200_Close | kospi_200_midnsmall_Close | kospi_200_exbig_Close | exchange_rate_usd_Close | exchange_rate_eur_Close | exchange_rate_jpy_Close | exchange_rate_cny_Close | comex_gold_Close   | comex_silver_Close | comex_copper_Close | platinum_Close     | palladium_Close    | crude_oil_Close     | rbob_gasoilne_Close | natural_gas_Close  | heating_oil_Close  | treasury_13w_Close    | treasury_5y_Close   | treasury_10y_Close  | treasury_30y_Close | treasury_krx_3y | treasury_krx_5y | treasury_krx_10y | treasury_krx_20y | treasury_krx_30y | vix_Close          | bitcoin_Close     | snp_500_Close     | dow_jones_Close | nasdaq_Close     | nyse_Close       | amex_Close         |
|---------|---------|---------|---------|------------|----------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------|--------------|--------------|-------------------|-------------------|--------------------|--------------------|--------------------|----------------------|----------------------|-----------------------|--------------------|--------------------|--------------------|----------------------|--------------------|---------------------|-------------------------|---------------------|-----------------------|--------|--------------------|--------------------|--------------------|--------------------|---------------|--------------------|-------------------|-------------------|-------------------|------------------|-------------------------|------------------|------------------|------------------|-----------------|------------------------|-----------------|---------------------------|-----------------------|-------------------------|-------------------------|-------------------------|-------------------------|--------------------|--------------------|--------------------|--------------------|--------------------|---------------------|---------------------|--------------------|--------------------|-----------------------|---------------------|---------------------|--------------------|-----------------|-----------------|------------------|------------------|------------------|--------------------|-------------------|-------------------|-----------------|------------------|------------------|--------------------|
| 2325.68 | 2329.58 | 2296.39 | 2326.13 | 396663000  | 0        | 2338.239999999998  | 2346.651000000001  | 2378.972666666667  | 2395.9330000000004 | 2416.570333333334  | 2439.0729999999994 | 2455.9350833333324 | 2335.3168292608857 | 2353.4768362263203 | 2369.5743411638455 | 2382.3130494573634 | 2400.1384073250906 | 2426.924478927261  | 2455.9350833333324 | 2331.5613333333717 | 2340.2732727272614 | 2354.6672499999954 | 2370.45319047618   | 2391.4003440860197 | 2423.4253224043678 | 2440.0657906336087 | 444730800.0  | 482631000.0  | 513389300.0  | 545187516.6666666 | 467189158.3333333 | 2502.008477486498  | 2395.9330000000004 | 2289.8575225135028 | -33.65353886512685   | -26.580702949204767  | -7.072835915922081    | 34.31505343940856  | 31.749102087711805 | 40.315704420267515 | 45.75384615384652    | 31.749102087711805 | 53.637192686642294  | 34.853966506931556      | -94.05207230033326  | -83.76371676584581    | 2607.1 | 34.14304666615668  | 9.525790298640755  | 38.07968428436444  | 28.554454841179258 | -806493000.0  | 256.70564000401646 | 3808594           | 248816            | 8351185           | 0                | 12408595                | 176093193751     | 2604822410       | 221582521557     | 0               | 400280537718           | 299.66          | 1073.04                   | 241.35                | 1115.04                 | 1302.92                 | 10.0744                 | 168.41                  | 1251.300048828125  | 16.104000091552734 | 852.4000244140625  | 2.9509999752044678 | 958.2999877929688  | 74.1500015258789    | 2.1791000366210938  | 2.9240000247955322 | 2.2093000411987305 | 1.8799999952316284    | 2.7309999465942383  | 2.8489999771118164  | 2.9830000400543213 | 2.124           | 2.354           | 2.555            | 2.561            | 2.552            | 16.09000015258789  | 6218.2998046875   | 2718.3701171875   | 24271.41015625  | 7510.2998046875  | 12504.25         | 2748.47998046875   |
| 2322.23 | 2327.59 | 2271.53 | 2271.54 | 393266000  | 1        | 2320.971999999998  | 2336.1810000000014 | 2366.9700000000003 | 2388.3595000000005 | 2410.2943333333333 | 2436.1959999999995 | 2454.144999999999  | 2314.0578861739236 | 2338.5792296397167 | 2357.3200485183647 | 2371.7632352233286 | 2391.8417358847623 | 2421.8299058476787 | 2452.8872307162524 | 2309.3280000000386 | 2326.6167272727166 | 2341.2381666666615 | 2358.6062380952276 | 2382.043548387095  | 2417.9324371584667 | 2437.017938016529  | 440368000.0  | 465475700.0  | 492206100.0  | 545236633.3333334 | 467707250.0       | 2506.557072813441  | 2388.3595000000005 | 2270.1619271865598 | -38.242878426353855  | -28.913138044634586  | -9.329740381719269    | 27.529276688753434 | 17.52169315785981  | 28.156337369132743 | 0.011470520761371358 | 17.52169315785981  | 0.0                 | 17.8790642288807        | -136.5068975225221  | -99.99519300100958    | 2607.1 | 36.51440076409937  | 8.275928024699379  | 35.35970683548126  | 30.519136638237878 | -1199759000.0 | 771.1538960048929  | 4639501           | 122533            | 7917446           | 0                | 12679480                | 215180531604     | 2164374815       | 201592339148     | 0               | 418937245567           | 292.93          | 1040.33                   | 236.02                | 1118.88                 | 1302.32                 | 10.0895                 | 167.8                   | 1239.800048828125  | 15.744000434875488 | 809.0              | 2.93149995803833   | 941.7999877929688  | 73.94000244140625   | 2.10479998588562    | 2.861999988555908  | 2.1558001041412354 | 1.8949999809265137    | 2.753000020980835   | 2.865999937057495   | 2.990000009536743  | 2.126           | 2.339           | 2.531            | 2.547            | 2.54             | 15.600000381469727 | 6614.18017578125  | 2726.7099609375   | 24307.1796875   | 7567.68994140625 | 12485.580078125  | 2721.06005859375   |
| 2264.74 | 2274.74 | 2243.9  | 2257.55 | 346884000  | 1        | 2278.6879999999983 | 2311.5730000000012 | 2329.190666666667  | 2361.1240000000007 | 2390.997666666667  | 2427.9919999999997 | 2448.4659166666656 | 2278.3041884959775 | 2304.958345910859  | 2326.708938753514  | 2344.007443083556  | 2368.8267797822655 | 2406.912594151451  | 2443.732051973694  | 2269.1386666667076 | 2292.169818181808  | 2308.080249999994  | 2325.8849523809413 | 2355.147161290321  | 2401.3820874316903 | 2427.7368994490357 | 363588800.0  | 418219900.0  | 466441050.0  | 535038750.0       | 468323750.0       | 2495.4597608977733 | 2361.1240000000007 | 2226.788239102228  | -45.91537223642081   | -36.284311642111874  | -9.631060594308934    | 26.14339477471161  | 16.96611776463064  | 16.75822973750213  | 15.931372549019745   | 16.96611776463064  | 0.0                 | 1.5661513841220867      | -137.12019877200382 | -91.55635283929229    | 2607.1 | 43.405460853819875 | 6.721312764374321  | 28.310960611352893 | 30.087023758822333 | -1495718000.0 | 591.7546960031614  | 2185055           | 199192            | 7199029           | 588              | 9583864                 | 111322617848     | 3101758210       | 203018046799     | 38394900        | 317480817757           | 291.63          | 1025.97                   | 233.89                | 1119.33                 | 1308.61                 | 10.1182                 | 168.65                  | 1257.300048828125  | 16.007999420166016 | 837.0999755859375  | 2.813999891281128  | 950.0999755859375  | 72.94000244140625   | 2.129300117492676   | 2.8369998931884766 | 2.1786999702453613 | 1.909999966621399     | 2.740999937057495   | 2.8399999141693115  | 2.953000068664551  | 2.095           | 2.334           | 2.545            | 2.556            | 2.549            | 14.970000267028809 | 6639.14013671875  | 2736.610107421875 | 24356.740234375 | 7586.43017578125 | 12585.2099609375 | 2749.260009765625  |
| 2261.44 | 2283.75 | 2247.35 | 2272.87 | 344433000  | 0        | 2268.035999999998  | 2303.1380000000013 | 2320.4460000000004 | 2351.2385000000004 | 2384.363           | 2425.380166666667  | 2446.4879166666656 | 2276.492792330652  | 2299.1241011997936 | 2319.9790714093247 | 2337.23244850417   | 2362.6360197963127 | 2402.5177549989444 | 2440.9078858253683 | 2267.199333333375  | 2285.132909090899  | 2301.0401666666608 | 2317.479809523798  | 2347.5260215053745 | 2396.2961202185757 | 2424.8344876033057 | 353142800.0  | 398936800.0  | 459955350.0  | 533207483.3333333 | 468074666.6666667 | 2480.9182390920814 | 2351.2385000000004 | 2221.5587609079193 | -45.81451406812039   | -38.190352127313574  | -7.624161940806815    | 30.95463421525518  | 22.110750359128883 | 16.912117292990292 | 34.61584418687989    | 22.110750359128883 | 100.0               | 33.333333333333265      | -100.10649956117005 | -78.63411756029215    | 2607.1 | 44.94594305059126  | 8.256530312210183  | 35.29874913911362  | 30.53795063319217  | -1151285000.0 | 34.91074400488287  | 2628640           | 372686            | 8166731           | 0                | 11168057                | 119908320532     | 4773676849       | 224061115144     | 0               | 348743112525           | 293.11          | 1054.57                   | 237.39                | 1115.52                 | 1310.39                 | 10.0988                 | 167.91                  | 1254.300048828125  | 15.980999946594238 | 844.2000122070312  | 2.812999963760376  | 955.0              | 73.80000305175781   | 2.1085000038146973  | 2.8580000400543213 | 2.1684000492095947 | 1.9049999713897705    | 2.7230000495910645  | 2.8310000896453857  | 2.940999984741211  | 2.106           | 2.355           | 2.557            | 2.564            | 2.554            | 13.369999885559082 | 6673.5            | 2759.820068359375 | 24456.48046875  | 7688.39013671875 | 12664.8798828125 | 2776.889892578125  |
| 2276.92 | 2294.61 | 2267.25 | 2285.8  | 352639000  | 0        | 2270.8879999999976 | 2295.930000000001  | 2314.416666666667  | 2342.9495000000006 | 2378.356           | 2422.7421666666664 | 2444.704999999999  | 2279.595194887101  | 2296.7015373452855 | 2315.706687483159  | 2332.3341200752016 | 2357.6788572288087 | 2398.6909433596347 | 2438.344119117511  | 2273.120666666709  | 2281.9805454545353 | 2296.7094166666607 | 2311.2475714285597 | 2341.1671182795676 | 2391.7197213114723 | 2422.178488980716  | 345017400.0  | 392692700.0  | 451079300.0  | 533511050.0       | 467313141.6666667 | 2466.9848206912693 | 2342.9495000000006 | 2218.914179308732  | -44.1819384198152    | -39.3886693858139    | -4.793269034001298    | 34.81425557981165  | 44.3913058612863   | 27.822724661682    | 82.62670084795911    | 44.3913058612863   | 100.0               | 66.6666666666666        | -59.419197770277925 | -67.9222171183585     | 2607.1 | 45.730106666518736 | 10.283409042788563 | 43.63740991489134  | 30.31095415939274  | -798646000.0  | 87.43317600619048  | 2095861           | 171087            | 7733663           | 0                | 10000611                | 109282791716     | 2662156630       | 204345701665     | 0               | 316290650011           | 295.2           | 1042.88                   | 238.4                 | 1113.32                 | 1308.26                 | 10.0435                 | 168.28                  | 1258.0999755859375 | 16.05299949645996  | 849.0              | 2.8389999866485596 | 962.0999755859375  | 73.8499984741211    | 2.1484999656677246  | 2.828000068664551  | 2.19569993019104   | 1.9149999618530273    | 2.752000093460083   | 2.859999895095825   | 2.9660000801086426 | 2.107           | 2.353           | 2.559            | 2.56             | 2.546            | 12.6899995803833   | 6741.75           | 2784.169921875    | 24776.58984375  | 7756.2001953125  | 12776.919921875  | 2771.699951171875  |
| 2299.09 | 2305.84 | 2292.13 | 2294.16 | 339919000  | 0        | 2275.1679999999974 | 2290.2540000000013 | 2311.3533333333335 | 2334.1500000000005 | 2372.801333333334  | 2420.1325          | 2443.0904166666655 | 2284.450129924734  | 2296.2394396461427 | 2313.013351547764  | 2328.698489591849  | 2353.5808664398533 | 2395.2636993150563 | 2435.9609105370564 | 2280.8780000000434 | 2281.6587272727174 | 2294.1773333333276 | 2306.6009523809407 | 2335.7351182795674 | 2387.5039125683024 | 2419.6901418732778 | 339795600.0  | 379593100.0  | 446677900.0  | 533236533.3333333 | 466442966.6666667 | 2445.123535583869  | 2334.1500000000005 | 2223.176464416132  | -41.73246247405132   | -39.85742800346138   | -1.875034470589938    | 37.25640375179238  | 66.12852889601716  | 44.21019503881084  | 81.14304165321234    | 66.12852889601716  | 100.0               | 99.99999999999993       | -22.749215452736983 | -60.32522892327137    | 2607.1 | 45.817175733027945 | 12.497780155946453 | 51.750452063827694 | 29.57731457657897  | -458727000.0  | 176.73109600692987 | 1393236           | 142213            | 5758129           | 0                | 7293578                 | 69234750800      | 1940137725       | 151400267615     | 0               | 222575156140           | 296.19          | 1043.51                   | 238.2                 | 1114.22                 | 1308.55                 | 10.0385                 | 168.06                  | 1253.800048828125  | 16.003000259399414 | 842.0              | 2.8285000324249268 | 945.0              | 74.11000061035156   | 2.1603000164031982  | 2.7880001068115234 | 2.2218000888824463 | 1.934999942779541     | 2.7720000743865967  | 2.872999906539917   | 2.9709999561309814 | 2.097           | 2.349           | 2.555            | 2.552            | 2.54             | 12.640000343322754 | 6329.9501953125   | 2793.840087890625 | 24919.66015625  | 7759.2001953125  | 12814.6396484375 | 2761.580078125     |
| 2277.22 | 2287.08 | 2262.77 | 2280.62 | 422989000  | 1        | 2278.199999999997  | 2284.113000000001  | 2305.800666666667  | 2324.7395000000006 | 2366.19            | 2417.4058333333332 | 2441.2920833333324 | 2283.173419949823  | 2293.399541528662  | 2308.9641826042935 | 2324.119585821197  | 2348.8737137663143 | 2391.504889501448  | 2433.393292181072  | 2282.6953333333777 | 2279.907090909081  | 2290.335666666661  | 2301.5028571428447 | 2329.7879354838688 | 2382.9297322404336 | 2417.0046804407702 | 361372800.0  | 369229500.0  | 437169050.0  | 534366550.0       | 466311408.3333333 | 2419.112415918624  | 2324.7395000000006 | 2230.3665840813774 | -40.41788773051485   | -39.969519948872076  | -0.4483677816427729   | 34.97118983748637  | 74.35097325649848  | 61.62360267126737  | 59.28317726832381    | 74.35097325649848  | 79.43658716537544   | 93.14552905512507       | -58.09613708974765  | -68.74627627883235    | 2607.1 | 46.42650007594193  | 11.55448957655508  | 48.053991202125715 | 29.70679210682332  | -881716000.0  | 154.63388000801206 | 3104692           | 115362            | 9543254           | 288              | 12763596                | 115408175713     | 2348972452       | 198583689547     | 1955520         | 316342793232           | 294.43          | 1039.07                   | 236.84                | 1128.23                 | 1317.1                  | 10.0722                 | 168.87                  | 1242.800048828125  | 15.732000350952148 | 831.0              | 2.7335000038146973 | 944.4000244140625  | 70.37999725341797   | 2.0613999366760254  | 2.8289999961853027 | 2.100800037384033  | 1.9199999570846558    | 2.740000009536743   | 2.8420000076293945  | 2.944999933242798  | 2.059           | 2.305           | 2.52             | 2.517            | 2.508            | 13.630000114440918 | 6394.7099609375   | 2774.02001953125  | 24700.44921875  | 7716.60986328125 | 12681.58984375   | 2728.7900390625    |
| 2285.93 | 2298.56 | 2277.73 | 2285.06 | 364408000  | 0        | 2283.701999999997  | 2281.1950000000015 | 2302.2826666666665 | 2317.8185000000003 | 2360.450333333333  | 2414.7783333333336 | 2439.469833333332  | 2283.8022799665487 | 2291.8832612507235 | 2305.976159778757  | 2320.399625266797  | 2344.7566999749392 | 2388.014893124351  | 2430.9415022276658 | 2284.982000000045  | 2280.079272727263  | 2287.743083333328  | 2297.7238571428447 | 2324.553741935482  | 2378.5905245901604 | 2414.422331955922  | 364877600.0  | 364233200.0  | 428717050.0  | 533080533.3333333 | 465976883.3333333 | 2401.9588682603658 | 2317.8185000000003 | 2233.678131739635  | -38.57315951001783   | -39.69024786110123   | 1.117088351083396     | 36.34990320344362  | 68.29959277780046  | 69.59303164343875  | 64.47255941186508    | 68.29959277780046  | 85.61514280881052   | 88.35057665806191       | -28.953282689458728 | -64.96723125372378    | 2607.1 | 46.38077056370553  | 13.783701590247693 | 56.10156325911675  | 29.072735527764504 | -517308000.0  | 48.48929600883275  | 5079902           | 191195            | 7143451           | 0                | 12414548                | 240267326793     | 1839124410       | 188625939914     | 0               | 430732391117           | 294.41          | 1041.29                   | 237.72                | 1124.58                 | 1312.66                 | 9.9905                  | 168.66                  | 1245.0             | 15.89799976348877  | 842.2999877929688  | 2.7679998874664307 | 956.2000122070312  | 70.33000183105469   | 2.071700096130371   | 2.796999931335449  | 2.1231000423431396 | 1.9279999732971191    | 2.755000114440918   | 2.8529999256134033  | 2.950000047683716  | 2.088           | 2.328           | 2.535            | 2.532            | 2.517            | 12.579999923706055 | 6228.81005859375  | 2798.2900390625   | 24924.890625    | 7823.919921875   | 12761.4599609375 | 2738.280029296875  |

## 2) Data Analysis Module
Prophet, AutoML, Natural Language Processing, Reinforcement Learning
## 3) Run Module
app.py
# 5. Development Notes

# Contributing
실용 중심 AI 개발자 양성 과정 씨에쓰리 산학프로젝트

# License & Reference
강화학습 모델 [QuantyLab](https://github.com/quantylab/rltrader)
