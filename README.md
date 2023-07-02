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
        alert(err);
      }
    }
  }

  return (
    <AppWrap>
      <div className = 'appContentWrap'>
        <input 
        placeholder="도시를 입력하세요"
        value={location}
        onChange={(e)=> setLocation(e.target.value)}
        type = 'text'
        onKeyDown={searchWeather}
        />
        {Object.keys(result).length!==0 && ( //빈 오브젝트가 아닐 때 
          <ResultWrap>
          <div className="city">{result.data.name}</div>
          <div className="temperature">{Math.round((result.data.main.temp-273.15)*10)/10}°C</div>
          <div className="sky">{result.data.weather[0].main}</div>
          </ResultWrap>
        )}
      </div>
    </AppWrap>
  );
}

export default App;

const AppWrap = styled.div`
  width: 100vw;
  height: 100vh;
  border: 1px red solid;

  .appContentWrap {
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
    padding: 20px;
  }
  input {
    padding: 16px;
    border: 2px black solid;
    border-radius: 16px;
  }
`;

const ResultWrap = styled.div`
  margin-top: 60px;
  padding: 10px;
  border: 1px black solid;
  border-radius: 8px;
  .city{
    font-size: 24px;
  }
  .temperature{
    font-size: 60px;
    margin-top: 8px;
  }
  .sky{
    font-size: 20px;
    text-aligh: right;
    margin-top: 8px;
  }
`;
```

# ❤️ 공공데이터 포털에서 API 가져오는 법 <br>



# ⭕ 결과 화면 <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/f184d53a-ab4b-4533-a88e-56b1252cb646) <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/10bda976-f8f5-421e-a817-87afa08b8c0e) <br>
