---
layout: single
title: "[Python] Pandas와 Matplotlib을 이용한 데이터 시각화 예제 (세계 top10 인구 변화)"
categories: [python]
tags: [Python, Pandas, Matplotlib]
header:
  teaser: /assets/images/teasers/teaser_python.webp
---

# Pandas와 Matplotlib를 이용한 데이터 시각화 예제 (세계 top10 인구 변화)

`Pandas`와 `Matplotlib`을 이용하여 세계 상위 10개국의 인구 변화를 line plot으로 시각화하는 예제를 만들어 보도록 하자.

시각화를 위해 jupyter notebook을 사용하였다.

## 0. 데이터 출처

[세계 인구 데이터](https://www.kaggle.com/datasets/sazidthe1/world-population-data)는 **Kaggle**에서 다운로드 받아서 사용할 수 있다.

## 1. 데이터 준비

```python
import sys
import pandas as pd
import matplotlib.pyplot as plt

plt.rcParams.update(
    {
        "font.family": "AppleGothic" if sys.platform == "darwin" else "Malgun Gothic",
        "font.size": 8,
        "figure.figsize": (12, 6),
        "axes.unicode_minus": False,
    }
)

# 데이터의 경로는 상황에 맞게 변경
origin = pd.read_csv("./world_population_data.csv", index_col=0)
origin.head()
```

### 출력 결과 확인 (상위 5개)

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cca3</th>
      <th>country</th>
      <th>continent</th>
      <th>2023 population</th>
      <th>2022 population</th>
      <th>2020 population</th>
      <th>2015 population</th>
      <th>2010 population</th>
      <th>2000 population</th>
      <th>1990 population</th>
      <th>1980 population</th>
      <th>1970 population</th>
      <th>area (km²)</th>
      <th>density (km²)</th>
      <th>growth rate</th>
      <th>world percentage</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>IND</td>
      <td>India</td>
      <td>Asia</td>
      <td>1428627663</td>
      <td>1417173173</td>
      <td>1396387127</td>
      <td>1322866505</td>
      <td>1240613620</td>
      <td>1059633675</td>
      <td>870452165</td>
      <td>696828385</td>
      <td>557501301</td>
      <td>3287590.00</td>
      <td>481</td>
      <td>0.81%</td>
      <td>17.85%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CHN</td>
      <td>China</td>
      <td>Asia</td>
      <td>1425671352</td>
      <td>1425887337</td>
      <td>1424929781</td>
      <td>1393715448</td>
      <td>1348191368</td>
      <td>1264099069</td>
      <td>1153704252</td>
      <td>982372466</td>
      <td>822534450</td>
      <td>9706961.00</td>
      <td>151</td>
      <td>-0.02%</td>
      <td>17.81%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>USA</td>
      <td>United States</td>
      <td>North America</td>
      <td>339996563</td>
      <td>338289857</td>
      <td>335942003</td>
      <td>324607776</td>
      <td>311182845</td>
      <td>282398554</td>
      <td>248083732</td>
      <td>223140018</td>
      <td>200328340</td>
      <td>9372610.00</td>
      <td>37</td>
      <td>0.50%</td>
      <td>4.25%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>IDN</td>
      <td>Indonesia</td>
      <td>Asia</td>
      <td>277534122</td>
      <td>275501339</td>
      <td>271857970</td>
      <td>259091970</td>
      <td>244016173</td>
      <td>214072421</td>
      <td>182159874</td>
      <td>148177096</td>
      <td>115228394</td>
      <td>1904569.00</td>
      <td>148</td>
      <td>0.74%</td>
      <td>3.47%</td>
    </tr>
    <tr>
      <th>5</th>
      <td>PAK</td>
      <td>Pakistan</td>
      <td>Asia</td>
      <td>240485658</td>
      <td>235824862</td>
      <td>227196741</td>
      <td>210969298</td>
      <td>194454498</td>
      <td>154369924</td>
      <td>115414069</td>
      <td>80624057</td>
      <td>59290872</td>
      <td>881912.00</td>
      <td>312</td>
      <td>1.98%</td>
      <td>3.00%</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 16 columns</p>
</div>

## 2. 데이터 전처리

상위 10개국의 데이터만 추출하고 연도의 컬럼을 `reverse(반전)` 시킨다.

```python
# rank 순으로 이미 정렬이 되어있기 때문에 따로 처리 없이 인덱스를 cca3(국가코드)로 변경
df = origin.copy().head(10).set_index("cca3")
# 모든 컬럼 반전
df = df[df.columns[::-1]]
df
```

### 출력 결과 확인

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>world percentage</th>
      <th>growth rate</th>
      <th>density (km²)</th>
      <th>area (km²)</th>
      <th>1970 population</th>
      <th>1980 population</th>
      <th>1990 population</th>
      <th>2000 population</th>
      <th>2010 population</th>
      <th>2015 population</th>
      <th>2020 population</th>
      <th>2022 population</th>
      <th>2023 population</th>
      <th>continent</th>
      <th>country</th>
    </tr>
    <tr>
      <th>cca3</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>IND</th>
      <td>17.85%</td>
      <td>0.81%</td>
      <td>481</td>
      <td>3287590.0</td>
      <td>557501301</td>
      <td>696828385</td>
      <td>870452165</td>
      <td>1059633675</td>
      <td>1240613620</td>
      <td>1322866505</td>
      <td>1396387127</td>
      <td>1417173173</td>
      <td>1428627663</td>
      <td>Asia</td>
      <td>India</td>
    </tr>
    <tr>
      <th>CHN</th>
      <td>17.81%</td>
      <td>-0.02%</td>
      <td>151</td>
      <td>9706961.0</td>
      <td>822534450</td>
      <td>982372466</td>
      <td>1153704252</td>
      <td>1264099069</td>
      <td>1348191368</td>
      <td>1393715448</td>
      <td>1424929781</td>
      <td>1425887337</td>
      <td>1425671352</td>
      <td>Asia</td>
      <td>China</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>4.25%</td>
      <td>0.50%</td>
      <td>37</td>
      <td>9372610.0</td>
      <td>200328340</td>
      <td>223140018</td>
      <td>248083732</td>
      <td>282398554</td>
      <td>311182845</td>
      <td>324607776</td>
      <td>335942003</td>
      <td>338289857</td>
      <td>339996563</td>
      <td>North America</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>IDN</th>
      <td>3.47%</td>
      <td>0.74%</td>
      <td>148</td>
      <td>1904569.0</td>
      <td>115228394</td>
      <td>148177096</td>
      <td>182159874</td>
      <td>214072421</td>
      <td>244016173</td>
      <td>259091970</td>
      <td>271857970</td>
      <td>275501339</td>
      <td>277534122</td>
      <td>Asia</td>
      <td>Indonesia</td>
    </tr>
    <tr>
      <th>PAK</th>
      <td>3.00%</td>
      <td>1.98%</td>
      <td>312</td>
      <td>881912.0</td>
      <td>59290872</td>
      <td>80624057</td>
      <td>115414069</td>
      <td>154369924</td>
      <td>194454498</td>
      <td>210969298</td>
      <td>227196741</td>
      <td>235824862</td>
      <td>240485658</td>
      <td>Asia</td>
      <td>Pakistan</td>
    </tr>
    <tr>
      <th>NGA</th>
      <td>2.80%</td>
      <td>2.41%</td>
      <td>246</td>
      <td>923768.0</td>
      <td>55569264</td>
      <td>72951439</td>
      <td>95214257</td>
      <td>122851984</td>
      <td>160952853</td>
      <td>183995785</td>
      <td>208327405</td>
      <td>218541212</td>
      <td>223804632</td>
      <td>Africa</td>
      <td>Nigeria</td>
    </tr>
    <tr>
      <th>BRA</th>
      <td>2.70%</td>
      <td>0.52%</td>
      <td>26</td>
      <td>8515767.0</td>
      <td>96369875</td>
      <td>122288383</td>
      <td>150706446</td>
      <td>175873720</td>
      <td>196353492</td>
      <td>205188205</td>
      <td>213196304</td>
      <td>215313498</td>
      <td>216422446</td>
      <td>South America</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>BGD</th>
      <td>2.16%</td>
      <td>1.03%</td>
      <td>1329</td>
      <td>147570.0</td>
      <td>67541860</td>
      <td>83929765</td>
      <td>107147651</td>
      <td>129193327</td>
      <td>148391139</td>
      <td>157830000</td>
      <td>167420951</td>
      <td>171186372</td>
      <td>172954319</td>
      <td>Asia</td>
      <td>Bangladesh</td>
    </tr>
    <tr>
      <th>RUS</th>
      <td>1.80%</td>
      <td>-0.19%</td>
      <td>9</td>
      <td>17098242.0</td>
      <td>130093010</td>
      <td>138257420</td>
      <td>148005704</td>
      <td>146844839</td>
      <td>143242599</td>
      <td>144668389</td>
      <td>145617329</td>
      <td>144713314</td>
      <td>144444359</td>
      <td>Europe</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>MEX</th>
      <td>1.60%</td>
      <td>0.75%</td>
      <td>66</td>
      <td>1964375.0</td>
      <td>50289306</td>
      <td>67705186</td>
      <td>81720428</td>
      <td>97873442</td>
      <td>112532401</td>
      <td>120149897</td>
      <td>125998302</td>
      <td>127504125</td>
      <td>128455567</td>
      <td>North America</td>
      <td>Mexico</td>
    </tr>
  </tbody>
</table>
</div>

## 3. 데이터 시각화

```python
# filter를 이용하여 컬럼명에 population이 포함된 컬럼만 추출한다.
# 속성 T는 transpose() 메서드에 대한 약어로 행과 열을 바꾼다.
plt.plot(df.filter(like="population").T, marker="o", label=df.index)
# 그래프의 제목
plt.title("연도에 따른 인구수 변화 (세계 인구 top10)")
# x축 라벨
plt.xlabel("연도")
# y축 라벨
plt.ylabel("인구수")
# y축 눈금 설정 (1e8은 1억을 의미하고 이를 15번 반복하면서 15억까지 표시한다.)
plt.yticks([1e8 * i for i in range(1, 16)], [f"{i}억명" for i in range(1, 16)])
# 그리드 표시
plt.grid()
# 범례 표시
plt.legend(title="국가", loc="upper left", bbox_to_anchor=(1, 1))
# 그래프 출력
plt.show()
plt.close()
```

### 출력 결과 확인

![Alt text](/assets/images/2024-01-07/02.png)

## 4. 최종 코드

```python
import sys
import pandas as pd
import matplotlib.pyplot as plt

plt.rcParams.update(
    {
        "font.family": "AppleGothic" if sys.platform == "darwin" else "Malgun Gothic",
        "font.size": 8,
        "figure.figsize": (12, 6),
        "axes.unicode_minus": False,
    }
)

origin = pd.read_csv("./world_population_data.csv", index_col=0)

df = origin.copy().head(10).set_index("cca3")
df = df[df.columns[::-1]]

plt.plot(df.filter(like="population").T, marker="o", label=df.index)
plt.title("연도에 따른 인구수 변화 (세계 인구 top10)")
plt.xlabel("연도")
plt.ylabel("인구수")
plt.yticks([1e8 * i for i in range(1, 16)], [f"{i}억명" for i in range(1, 16)])
plt.grid()
plt.legend(title="국가", loc="upper left", bbox_to_anchor=(1, 1))
plt.show()
plt.close()
```
