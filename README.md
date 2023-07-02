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
1. useState를 사용하여 location과 result라는 두 개의 상태 변수를 선언합니다. location은 사용자가 입력한 도시 이름을 저장하고, result는 API에서 받아온 날씨 정보를 저장합니다.<br>
2. API_KEY 상수에 OpenWeatherMap API의 개인 키를 저장합니다.<br>
3. searchWeather 함수는 사용자가 입력창에서 엔터를 입력하면 실행되는 이벤트 핸들러입니다. axios 라이브러리를 사용하여 API를 호출하고, API 응답을 받아와 result 상태 변수에 저장합니다.<br>
4. result 상태 변수에 데이터가 있는 경우, ResultWrap 컴포넌트를 렌더링합니다. result 객체는 API 응답 데이터를 담고 있으며, 여기서는 도시 이름, 온도, 날씨 상태를 표시합니다. <br>
5. AppWrap과 ResultWrap은 styled-components를 사용하여 스타일링한 컴포넌트입니다. AppWrap은 애플리케이션 전체를 감싸는 컨테이너로, 앱 컨텐츠를 중앙에 배치하기 위해 transform과 position 스타일을 사용합니다. ResultWrap은 결과를 표시하는 부분의 스타일을 지정합니다. <br><br>


# ⭕ 결과 화면 <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/f184d53a-ab4b-4533-a88e-56b1252cb646) <br>
![image](https://github.com/An-jisu/React_weather_API/assets/70849122/10bda976-f8f5-421e-a817-87afa08b8c0e) <br>
