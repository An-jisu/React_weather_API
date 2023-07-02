# React와 styled-components를 사용하여 간단한 날씨 웹 애플리케이션 만드는 예제 <br>
-> 사용자가 도시 이름 입력하면, 날씨 open api 이용하여 해당 도시의 날씨 정보를 가져옴<br><br>

# 😀 날씨 API 가져오는 법 <br>
### 1. API key 받기:'https://openweathermap.org/api/one-call-3'접속하여 회원가입 시, api key 생성됨 <br>
### 2. API doc: 필요한 데이터 api의 doc에 들어가기<br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/c37663ae-49a6-43ad-b6ed-3dc897202cc0) <br>
### 3. api call 주소 가져오기: <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/eeac8de3-136a-4bbf-85a1-0eb1804c5b48) <br>
### 4. 코드에 3의 주소에 api키를 넣어서 axios와 get을 이용해 가져오기 <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/caf0e6a3-49f4-498d-9e19-2a09f3aa6cfb) <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/0879ab26-a4e2-4c54-a00b-1ad7cd39811a)<br><br>

# 🔶 코드 explanation <br>
```
import {useState} from 'react';
import styled from "styled-components";
import axios from 'axios';

function App() {
  const API_KEY = "f4686a4143efca276b81e67b2479e4b2";
  const [location, setLocation] = useState('');
  const [result, setResult] = useState({});
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${location}&appid=${API_KEY}`;
  
  const searchWeather = async(e) => {
    if(e.key==='Enter'){
      try {
        const data = await axios({
          method: 'get',
          url: url
        })
        console.log(data)
        setResult(data);
      }
      catch(err){
        alert(시<br><br>


# ⭕ 결과 화면 <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/f184d53a-ab4b-4533-a88e-56b1252cb646) <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/10bda976-f8f5-421e-a817-87afa08b8c0e) <br>
