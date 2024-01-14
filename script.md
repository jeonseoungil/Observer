java script로 구현 후 리엑트로 변경 / 해당 파일은 javascript 코드 <br>

<script> <br>
        let num = document.querySelectorAll('h2'); <br>
        let obser = document.querySelectorAll('div'); <br>
        let animationDuration = 3000;  <br>
        let intervalDuration = 10;  <br> <br>

        /* 해당 숫자들이 숫자 증가애니메이션 효과 (IntersectionObserver에서 해당 함수 호출됨 )  */ <br>
        function animateNumber(elements) { <br>
                if (elements.getAttribute('data-num')) { <br>
                    let targetNum = parseInt(elements.getAttribute('data-num')); <br>
                    let currentNum = 0; <br>
                    let increment = (targetNum / (animationDuration / intervalDuration)); <br> <br>

                    let intervalId = setInterval(() => { <br>
                        currentNum += increment; <br>
                        if (currentNum >= targetNum) { <br>
                            currentNum = targetNum; <br>
                            clearInterval(intervalId); <br>
                        } <br>
                       elements.textContent = Math.floor(currentNum); <br>
                    }, intervalDuration); <br> <br>

                } <br>
        } <br>
        /* IntersectionObserver를 사용하여 해당 요소들이 화면에 50%이상 나타나야 나타남  */ <br>
        function Observe(element) { <br>
            let obver = new IntersectionObserver(entries => { <br>
                entries.forEach(item => { <br>
                    if (item.isIntersecting) { <br>
                        item.target.style.opacity = 1; <br>
                        item.target.style.transform ='translateY(0)'; <br>
                        animateNumber(item.target);  <br>
                    } <br>
                }); <br>
            }, { <br>
                threshold: 0.5 <br>
            }); <br>
 <br>
            element.forEach(item => { <br>
                obver.observe(item); <br>
            }); <br>
        } <br>
 <br>
        Observe(obser); <br>
        Observe(num); <br>
 <br>
        window.addEventListener('scroll', () => { <br>
            if (window.innerHeight + window.scrollY >= document.body.offsetHeight) { <br>
                contentContainer.innerHTML += ` <br>
                    <div class="content"></div> <br>
                    <div class="content"></div> <br>
                    <div class="content"></div> <br>
                    <div class="content"></div> <br>
                    <div class="content"></div> <br>
                `; <br>
                let newObser = document.querySelectorAll('.content:not(.observed)'); <br>
                Observe(newObser); <br>
                newObser.forEach(content => content.classList.add('observed')); <br>
            } <br>
        }); <br>
    </script> <br>
