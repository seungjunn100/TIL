버블링 a버튼을 클릭했을 때 그 상위의 버튼도 클릭한걸로 간주하고 상위의 클릭 이벤트가 발생하며 그 다음 상위의 클릭 이벤트도 발생.. 쭈욱 발생한다. 이것이 이벤트 전파 현상이다.

document.querySelector('button').addEventListener('click', a); // 버블링
document.querySelector('button').addEventListener('click', a, false); // 버블링

캡처링은 상위의 버튼을 클릭했을 때 위에서 부터 하위의 클릭 이벤트가 호출되는 전파가 진행된다.

document.querySelector('button').addEventListener('click', a, true); // 캡처링

버튼을 누르는건 똑같다.

버튼을 누르면 캡처링은 상위의 이벤트부터 처리하고, 버블링은 버튼부터 상위까지 이벤트가 처리된다.
대부분은 캡처링은 사용되지 않음.