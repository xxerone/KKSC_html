var isBool;
let today = new Date();
var spanEl2; // 원래 const였음, 여기 선언도 아님
let currentDate;

const event_name = document.querySelector('.event_name');
const Today = document.querySelector('.today');

let DATA = {
  // todolist 목록
};

Date.prototype.format = function () {
  var yyyy = this.getFullYear();
  var month = (this.getMonth() + 1);
  var dd = this.getDate();
  var format = [yyyy, month, dd].join('-');
  return format;
}

Date.prototype.format2 = function () {
  var yyyy = this.getFullYear();
  var month = (this.getMonth() + 1);
  var format = [yyyy, month].join('-');
  return format;
}



//main.js 확인 완료
window.onload = function () {
const calendarBody = document.querySelector('.calendar-body');
const prevEl = document.querySelector('.prev');
const nextEl = document.querySelector('.next');
const inputBox = document.querySelector('.input-box');
const inputBtn = document.querySelector('.input-btn');
const inputList = document.querySelector('.todoList');
const showList = document.querySelector('.showList');
const listText = document.querySelector('.listText');
const createDate = document.querySelector('.createDate');
const bgblack = document.querySelector('.bgblack'); // 없앴다가 살린거
const closedBtn = document.querySelector('.closed'); // 없앴다가 살린거
// let currentDate;

buildCalendar();
function buildCalendar() {
  let firstDate = new Date(today.getFullYear(), today.getMonth(), 1);
  const monthList = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
  const leapYear = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
  const notLeapYear = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
  const headerYear = document.querySelector('.current-year-month');
  
  if (firstDate.getFullYear() % 4 === 0) {
    pageYear = leapYear;
  } 
  
  else {
    pageYear = notLeapYear;
  }
  
  headerYear.innerHTML = `${monthList[firstDate.getMonth()]}&nbsp;&nbsp;&nbsp;&nbsp;${today.getFullYear()}`;
  makeElement(firstDate);
  // currentDateget();
  // showMain();
  currentDate = today.format();
  resetInsert();
}

  /*
  function showMain() {
  const mainDay = document.querySelector('.main-day');
  const mainDate = document.querySelector('.main-date');
  const dayList = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  mainDay.innerHTML = dayList[today.getDay()];
  mainDate.innerHTML = today.getDate();
}
*/
  
function makeElement(firstDate) {
  let weekly = 100;
  let dateSet = 1;
  for (let i = 0; i < 5; i++) {
    let weeklyEl = document.createElement('div');
    weeklyEl.setAttribute('class', weekly);
    weeklyEl.setAttribute('id', "weekly");
    for (let j = 0; j < 7; j++) 
    {
      if (i === 0 && j < firstDate.getDay() || dateSet > pageYear[firstDate.getMonth()]) 
      {
        let dateEl = document.createElement('div');
        weeklyEl.appendChild(dateEl);
      } 
      
      else 
      {
        let dateEl = document.createElement('div');
        dateEl.textContent = dateSet;
        dateEl.setAttribute('class', dateSet);
        dateEl.setAttribute('id', `${today.format2()}-${dateSet}`);
        weeklyEl.appendChild(dateEl);
        dateSet++;
      }
    }
    weekly++; calendarBody.appendChild(weeklyEl);
  }
// let clickedDate = document.getElementsByClassName(today.getDate());
  // clickedDate[0].classList.add('active');
}

function removeCalendar() {
  let divEls = document.querySelectorAll('.calendar-body > #weekly > div');
  for (let i = 0; i < divEls.length; i++)   {
    divEls[i].remove();
  }
}

/*
function currentDateget() {
  // format()을 이용해서 현재 날짜를 보기좋게 출력해주기 위해 사용.
  currentDate = today.format();
}
*/
  
function updateCalendar() {
  let event_name = document.querySelector('.event_name'); 
  // event_name 요소 선택
  event_name.innerHTML = ''; 
  // 기존 내용을 비움
          
  if (DATA[currentDate]) 
  {
    for (let i = 0; i < DATA[currentDate].length; i++) 
    {
      event_name.innerHTML += DATA[currentDate][i].todo + '<br>'; 
        // 각 일정을 새로운 줄에 추가
    }
  } 
      
  else 
  {
    event_name.innerHTML = "일정 없음";
  }
  console.log(event_name.innerHTML);
}
  
prevEl.addEventListener('click', function () {
  today = new Date(today.getFullYear(), today.getMonth() - 1, today.getDate());
  removeCalendar();
  buildCalendar();
  resetInsert();
  redrawLi(); // 세미콜론 붙임
});
  
nextEl.addEventListener('click', function () {
  today = new Date(today.getFullYear(), today.getMonth() + 1, today.getDate());
  removeCalendar();
  buildCalendar();
  resetInsert();
  redrawLi(); // 세미콜론 붙임
});

calendarBody.addEventListener('click', function (e) {
  let target = e.target;
  let eachDate = document.querySelectorAll('.calendar-body > #weekly > div');
  // if (e.target.innerHTML === '') return;
  for (let i = 0; i < eachDate.length; i++) 
  {
   eachDate[i].classList.remove('active');
   isBool = false;
  }
  
  isBool = true;
  target.classList.add('active');
  today = new Date(today.getFullYear(), today.getMonth(), target.innerHTML);
  // showMain();
  // currentDateget();
  currentDate = today.format();
  redrawLi();
  resetInsert();
});

inputBtn.addEventListener('click', function (e) {
  e.preventDefault();
  let inputValue = inputBox.value;
  insertTodo(inputValue);
});

closedBtn.addEventListener('click', function(e){
  showList.style.display = "none";
  bgblack.style.display = "none";
});
  
function insertTodo(text) {
  let todoObj = {
    todo: text,
  }
  
  if (!DATA[currentDate]) 
  {
    DATA[currentDate] = [];
    DATA[currentDate].push(todoObj);
    
    
    
  } 
  
  else 
  {
    DATA[currentDate].push(todoObj);
    
    
    
  }
  const liEl = document.createElement('li');
  const spanEl = document.createElement('span');
  const delBtn = document.createElement('button');
  
  delBtn.innerText = "DEL";
  delBtn.setAttribute('class', 'del-data');
  spanEl.innerHTML = text;
  liEl.appendChild(spanEl);
  liEl.appendChild(delBtn);
  inputList.appendChild(liEl);
  liEl.setAttribute('id', DATA[currentDate].length);
  delBtn.addEventListener('click', delWork);
  liEl.addEventListener('dblclick', showTodo);
  todoObj.id = DATA[currentDate].length;
  // save();
  localStorage.setItem(currentDate, JSON.stringify(DATA[currentDate]));
  inputBox.value = '';
}

function redrawLi() {
  let liEl = document.querySelectorAll('LI');
  for (let i = 0; i < liEl.length; i++) {
    inputList.removeChild(liEl[i]);
  }
  for (let todoList in DATA) {
    if (todoList === currentDate) {
      for (let i = 0; i < DATA[todoList].length; i++) {
        const liEl2 = document.createElement('li');
        // const spanEl2 = document.createElement('span');
        spanEl2 = document.createElement('span');
        const delBtn2 = document.createElement('button');
        delBtn2.innerText = "DEL";
        delBtn2.setAttribute('class', 'del-data');
        spanEl2.innerHTML = DATA[todoList][i].todo;
        liEl2.appendChild(spanEl2);
        liEl2.appendChild(delBtn2);
        inputList.appendChild(liEl2);
        liEl2.setAttribute('id', DATA[todoList][i].id);
        delBtn2.addEventListener('click', delWork);
        liEl2.addEventListener('dblclick', showTodo);
      }
    }
  }
}

function resetInsert() {
  let storeObj = localStorage.getItem(currentDate);
  if (storeObj !== null) {
    let liEl = document.querySelectorAll('LI');
    
    for (let i = 0; i < liEl.length; i++)     {
      inputList.removeChild(liEl[i]);
    }
    
    const parsed = JSON.parse(localStorage.getItem(currentDate));
    
    parsed.forEach(function (todo) {
      if (todo) {
        let lili = document.createElement('li');
        let spanspan = document.createElement('span');
        let deldel = document.createElement('button');
        deldel.setAttribute('class', 'del-data');
        deldel.innerText = "DEL";
        lili.setAttribute('id', todo.id);
        spanspan.innerHTML = todo.todo;
        lili.appendChild(spanspan);
        lili.appendChild(deldel);
        inputList.appendChild(lili);
        deldel.addEventListener('click', delWork);
        lili.addEventListener('dblclick', showTodo);
      }
    });
  }
}
resetInsert();

function delWork(e) {
  e.preventDefault();
  let delParentLi = e.target.parentNode;
  inputList.removeChild(delParentLi);
  const cleanToDos = DATA[currentDate].filter(function (todo)     {
    return todo.id !== parseInt(delParentLi.id);
  });
  DATA[currentDate] = cleanToDos;
  // save();
  localStorage.setItem(currentDate, JSON.stringify(DATA[currentDate]));
}

function showTodo(e){
  showList.style.display = "block"; 
  bgblack.style.display = "block"; 
  listText.textContent = e.target.textContent;
  createDate.textContent = currentDate;
}
  
}

/*
function save() {
  localStorage.setItem(currentDate, JSON.stringify(DATA[currentDate]));
}
*/





var inp = document.querySelector('#userName');
var but = document.querySelector('#userButton');
var namelist = document.querySelector('#nameList');

// .wrapper2 클래스를 가진 요소를 선택
    const wrapper = document.querySelector('.wrapper2');
    
    if (wrapper) {
      // 클릭 이벤트 리스너 추가
      wrapper.addEventListener('click', function() {
        if (Today && isBool) {
            Today.innerHTML = today;

            // 텍스트 내용 가져오기
            // let spanTextContent = spanEl2.textContent;
            
            //event_name.innerHTML = spanTextContent;
          } 
        else {
            console.error('.today 클래스를 가진 요소를 찾을 수 없습니다.');
          }
      });
    } 
    else {
      console.log('.wrapper2 클래스를 가진 요소를 찾을 수 없습니다.');
    }

function del(){
  var cla = document.querySelectorAll('.num'); 
  for(var i = 0; i < cla.length; i++){
    cla[i].addEventListener('click', function(){
        console.log(this);
        if(this.parentNode){
          this.parentNode.remove();
        }
    })
  }
};

but.addEventListener('click', function() 
{
    if(inp.value != null) 
    {
    var p = document.createElement('p');
    namelist.appendChild(p);
    p.textContent = inp.value;
    var span = document.createElement('span');
    p.appendChild(span);
    span.textContent = ' X';
    span.setAttribute('class', 'num');
    inp.value =''; //없앰
    
       // 새로 추가한 내용
      var i = 0;
      var paragraphs = document.getElementsByTagName('p');
      var text = paragraphs[i].textContent;
      alert(text);
      i++;
      if (paragraphs[i].textContent === paragraphs[i-1].textContent) {
        alert("같애");
      }
      
    inp.focus();
    namelist.insertBefore(p, namelist.childNodes[0]);
    }
  del();
});
