<!doctype html>
<html lang="az">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>EduTest.az — Demo</title>
  <meta name="description" content="EduTest.az — onlayn testlər və nəticə analizi (demo)" />
  <style>
    :root{
      --primary:#1565c0; /* mavi */
      --accent:#0b72b6;
      --muted:#6b7280;
      --bg:#f6fbff;
      --card:#ffffff;
      --radius:12px;
      --shadow: 0 6px 20px rgba(16,24,40,0.08);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
    }
    *{box-sizing:border-box}
    body{margin:0;background:var(--bg);color:#0f172a}
    header{background:linear-gradient(90deg,var(--primary),var(--accent));color:#fff;padding:20px;border-radius:0 0 18px 18px}
    .container{max-width:1024px;margin:20px auto;padding:16px}
    .brand{display:flex;gap:12px;align-items:center}
    .logo{width:56px;height:56px;border-radius:10px;background:#fff;display:flex;align-items:center;justify-content:center;color:var(--primary);font-weight:700}
    h1{margin:0;font-size:20px}
    p.lead{margin:6px 0 0;color:rgba(255,255,255,0.9)}

    .grid{display:grid;grid-template-columns:1fr 320px;gap:18px;margin-top:18px}
    .card{background:var(--card);border-radius:var(--radius);box-shadow:var(--shadow);padding:16px}
    .nav{display:flex;gap:8px;flex-wrap:wrap}
    .btn{background:var(--primary);color:#fff;padding:10px 12px;border-radius:10px;border:none;cursor:pointer}
    .muted{color:var(--muted)}

    .subject-list{display:flex;gap:8px;flex-wrap:wrap}
    .subject{padding:10px 12px;border-radius:10px;background:#eef6ff;border:1px solid rgba(21,101,192,0.08);cursor:pointer}
    .subject.active{background:var(--primary);color:#fff}

    .test-list{display:flex;flex-direction:column;gap:8px}
    .test-item{display:flex;justify-content:space-between;align-items:center;padding:12px;border-radius:10px;border:1px solid #eef2ff}

    .center{display:flex;align-items:center;justify-content:center}

    /* test runner */
    .question{margin:12px 0}
    .options{display:flex;flex-direction:column;gap:8px}
    .option{padding:12px;border-radius:10px;border:1px solid #e6eefc;cursor:pointer}
    .option.selected{background:#e9f4ff;border-color:var(--primary)}
    .timer{font-weight:600;color:var(--muted)}

    footer{margin-top:20px;text-align:center;color:var(--muted);font-size:13px;padding:20px}

    @media(max-width:880px){
      .grid{grid-template-columns:1fr;}
      .logo{width:44px;height:44px}
    }
  </style>
</head>
<body>
  <header>
    <div class="container brand">
      <div class="logo">ET</div>
      <div>
        <h1>EduTest.az — Demo</h1>
        <p class="lead">Onlayn testlər, nəticə analizi və premium resurslar (demo)</p>
      </div>
    </div>
  </header>

  <main class="container">
    <div class="grid">
      <section>
        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <h2 style="margin:0 0 6px 0">Fənlər</h2>
              <div class="muted">Seçdiyin fənn üzrə testləri başla</div>
            </div>
            <div>
              <button class="btn" id="open-random">Sınaq Testi Başla</button>
            </div>
          </div>

          <div style="margin-top:14px">
            <div class="subject-list" id="subjects"></div>
          </div>

          <hr style="margin:18px 0;border:none;border-top:1px solid #eef2ff" />

          <h3 style="margin:0 0 8px 0">Testlər</h3>
          <div class="test-list" id="test-list"></div>

        </div>

        <div class="card" style="margin-top:14px" id="runner-card" hidden>
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <strong id="test-title">Test adı</strong>
              <div class="muted" id="test-meta">5 sual · 5 dəq</div>
            </div>
            <div class="timer" id="timer">--:--</div>
          </div>

          <div id="question-area" style="margin-top:12px"></div>

          <div style="display:flex;justify-content:space-between;margin-top:12px">
            <button class="btn" id="prev-q">Geri</button>
            <div style="display:flex;gap:8px">
              <button class="btn" id="next-q">Növbəti</button>
              <button style="background:#e6eefc;color:var(--primary);border:none;padding:10px 12px;border-radius:10px;cursor:pointer" id="end-test">Testi Bitir</button>
            </div>
          </div>
        </div>

        <div class="card" style="margin-top:14px" id="result-card" hidden>
          <h3>Nəticən</h3>
          <div id="result-summary"></div>
          <div style="margin-top:12px;display:flex;gap:8px">
            <button class="btn" id="retry">Yenidən Sına</button>
            <button style="background:#fff;border:1px solid var(--primary);color:var(--primary);padding:8px 12px;border-radius:10px;cursor:pointer" id="save-result">Nəticəni Saxla</button>
          </div>
        </div>

      </section>

      <aside>
        <div class="card">
          <h3>Premium</h3>
          <p class="muted">Premium abunəlik əlavə materiallar, çətin testlər və PDF paketləri verir.</p>
          <div style="margin-top:12px;display:flex;gap:8px">
            <button class="btn" id="buy-premium">Abunə ol (5 AZN)</button>
          </div>
          <hr style="margin:12px 0;border:none;border-top:1px solid #f1f5f9" />
          <h4>Tez başla</h4>
          <div style="display:flex;flex-direction:column;gap:6px;margin-top:8px">
            <button style="padding:10px;border-radius:8px;border:1px dashed #e6eefc;background:transparent;cursor:pointer" id="quick-math">Riyaziyyat Testi</button>
            <button style="padding:10px;border-radius:8px;border:1px dashed #e6eefc;background:transparent;cursor:pointer" id="quick-az">Azərbaycan Dili</button>
          </div>
        </div>

        <div class="card" style="margin-top:14px">
          <h4>Keçmiş nəticələr</h4>
          <div id="saved-results" class="muted">Saxlanılan nəticə yoxdur</div>
        </div>

      </aside>
    </div>

    <footer>
      Demo sayt — bu kod sadəcə front-end nümunəsidir. Əgər backend, ödəmə və istifadəçi hesabları əlavə etmək istəyirsən, mən kömək edə bilərəm.
    </footer>
  </main>

  <script>
    // Demo data: suallar və testlər
    const DB = {
      subjects:[
        {id:'math',name:'Riyaziyyat'},
        {id:'aze',name:'Azərbaycan Dili'},
        {id:'eng',name:'İngilis Dili'}
      ],
      tests:[
        {id:'math-1',subject:'math',title:'Riyaziyyat: Asan test',duration:300,level:'asan',premium:false,questions:[
          {q:'2+2 = ?',choices:['3','4','5','6'],answer:1,explain:'2 + 2 = 4'},
          {q:'5 - 3 = ?',choices:['1','2','3','4'],answer:1,explain:'5 - 3 = 2'},
          {q:'3 * 3 = ?',choices:['6','8','9','12'],answer:2,explain:'3 × 3 = 9'}
        ]},
        {id:'aze-1',subject:'aze',title:'Azərbaycan Dili: Qrammatika',duration:300,level:'orta',premium:false,questions:[
          {q:"'Kitab' sözünün çoxluğu necədir?",choices:['Kitablar','Kitablarlar','Kitabs','Kitab-ler'],answer:0,explain:'Doğru forma: Kitablar'},
          {q:'İstifadə olunan düzgün vurğu hansıdır?',choices:['İlk hecada','Axırıncı hecada','Orta hecada','Vurğu yoxdur'],answer:0,explain:'Azerbaycan dilində bir çox söz ilk hecada vurğulanır.'}
        ]},
        {id:'eng-1',subject:'eng',title:'English: Beginner',duration:300,level:'asan',premium:true,questions:[
          {q:'What is the plural of "mouse"?',choices:['mouses','mice','mousees','meese'],answer:1,explain:'Plural of mouse is mice.'}
        ]}
      ]
    }

    // App state
    const state = {subject:null,test:null,idx:0,answers:{},timer:null,timeLeft:0}

    // Elements
    const subjectsEl = document.getElementById('subjects')
    const testListEl = document.getElementById('test-list')
    const runnerCard = document.getElementById('runner-card')
    const testTitleEl = document.getElementById('test-title')
    const testMetaEl = document.getElementById('test-meta')
    const timerEl = document.getElementById('timer')
    const questionArea = document.getElementById('question-area')
    const resultCard = document.getElementById('result-card')
    const resultSummary = document.getElementById('result-summary')
    const savedResultsEl = document.getElementById('saved-results')

    function init(){
      renderSubjects()
      renderTests()
      bindUI()
      loadSavedResults()
    }

    function renderSubjects(){
      subjectsEl.innerHTML = ''
      DB.subjects.forEach(s=>{
        const btn = document.createElement('div')
        btn.className='subject'
        btn.textContent = s.name
        btn.onclick = ()=>{ selectSubject(s.id, btn) }
        subjectsEl.appendChild(btn)
      })
    }

    function selectSubject(id,el){
      state.subject = id
      document.querySelectorAll('.subject').forEach(x=>x.classList.remove('active'))
      el.classList.add('active')
      renderTests()
    }

    function renderTests(){
      testListEl.innerHTML = ''
      const tests = DB.tests.filter(t=> state.subject? t.subject===state.subject:true)
      tests.forEach(t=>{
        const div = document.createElement('div')
        div.className='test-item'
        div.innerHTML = `<div><strong>${t.title}</strong><div class='muted'>${t.questions.length} sual · ${(t.duration/60).toFixed(0)} dəq ${t.premium? '· Premium':''}</div></div>`
        const actions = document.createElement('div')
        const start = document.createElement('button')
        start.className='btn'
        start.textContent='Başla'
        start.onclick = ()=> startTest(t.id)
        actions.appendChild(start)
        div.appendChild(actions)
        testListEl.appendChild(div)
      })
    }

    function startTest(testId){
      const t = DB.tests.find(x=>x.id===testId)
      if (!t) return
      if (t.premium && !isPremium()){
        if (!confirm('Bu test premiumdur. Premium almaq istəyirsiniz?')) return
        // in demo: simulate buy
        buyPremium()
        if (!isPremium()) return
      }
      state.test = t
      state.idx = 0
      state.answers = {}
      state.timeLeft = t.duration
      showRunner()
      renderQuestion()
      startTimer()
    }

    function showRunner(){
      runnerCard.hidden = false
      resultCard.hidden = true
      testTitleEl.textContent = state.test.title
      testMetaEl.textContent = `${state.test.questions.length} sual · ${(state.test.duration/60).toFixed(0)} dəq` 
    }

    function renderQuestion(){
      const q = state.test.questions[state.idx]
      questionArea.innerHTML = ''
      const elQ = document.createElement('div')
      elQ.className='question'
      elQ.innerHTML = `<div style='font-weight:700'>${state.idx+1}. ${q.q}</div><div class='muted' style='margin-top:6px'>Açıqlama: <span id='q-explain' class='muted' style='opacity:0.85'>${q.explain}</span></div>`
      questionArea.appendChild(elQ)

      const opts = document.createElement('div')
      opts.className='options'
      q.choices.forEach((c,i)=>{
        const o = document.createElement('div')
        o.className='option'
        o.textContent = c
        if (state.answers[state.idx]===i) o.classList.add('selected')
        o.onclick = ()=>{
          state.answers[state.idx]=i
          document.querySelectorAll('.option').forEach(x=>x.classList.remove('selected'))
          o.classList.add('selected')
        }
        opts.appendChild(o)
      })
      questionArea.appendChild(opts)
    }

    function nextQuestion(){
      if (state.idx < state.test.questions.length-1){
        state.idx++
        renderQuestion()
      } else {
        endTest()
      }
    }
    function prevQuestion(){
      if (state.idx>0){ state.idx--; renderQuestion() }
    }

    function endTest(){
      stopTimer()
      showResult()
    }

    function showResult(){
      runnerCard.hidden = true
      resultCard.hidden = false
      const total = state.test.questions.length
      let correct=0
      const details = []
      state.test.questions.forEach((q,i)=>{
        const sel = state.answers[i]
        const ok = sel===q.answer
        if (ok) correct++
        details.push({q:q.q,sel: sel!=null? q.choices[sel] : 'Seçilməyib',ans:q.choices[q.answer],ok})
      })
      const percent = Math.round(correct/total*100)
      resultSummary.innerHTML = `<div><strong>Sənin nəticən: ${correct}/${total} — ${percent}%</strong></div>`
      const det = document.createElement('div')
      det.style.marginTop='8px'
      det.innerHTML = details.map(d=>`<div style='padding:8px;border-radius:8px;border:1px solid #f1f5f9;margin-top:6px'><div style='font-weight:600'>${d.q}</div><div class='muted'>Sənin cavab: ${d.sel} · Doğru cavab: ${d.ans}</div></div>`).join('')
      resultSummary.appendChild(det)
    }

    function calculateScore(){
      // already done in showResult — separated for extension
    }

    // Timer
    function startTimer(){
      updateTimerDisplay()
      state.timer = setInterval(()=>{
        state.timeLeft--
        if (state.timeLeft<=0){ stopTimer(); endTest(); }
        updateTimerDisplay()
      },1000)
    }
    function stopTimer(){ if (state.timer) clearInterval(state.timer); state.timer=null }
    function updateTimerDisplay(){
      const mm = Math.floor(state.timeLeft/60).toString().padStart(2,'0')
      const ss = (state.timeLeft%60).toString().padStart(2,'0')
      timerEl.textContent = mm+':'+ss
    }

    // Premium (demo using localStorage)
    function isPremium(){ return localStorage.getItem('edutest_premium')==='1'}
    function buyPremium(){ localStorage.setItem('edutest_premium','1'); alert('Premium alındı — demo: 30 gün'); renderTests(); }

    // Saved results
    function saveResult(){
      const saved = JSON.parse(localStorage.getItem('edutest_saved')||'[]')
      const summary = {testId:state.test.id,title:state.test.title,correct: (Array.from(Object.keys(state.test.questions)).reduce((acc,_,i)=> acc + (state.answers[i]===state.test.questions[i].answer?1:0),0)),time: (new Date()).toISOString()}
      saved.push(summary)
      localStorage.setItem('edutest_saved', JSON.stringify(saved))
      loadSavedResults()
      alert('Nəticə saxlanıldı')
    }
    function loadSavedResults(){
      const saved = JSON.parse(localStorage.getItem('edutest_saved')||'[]')
      if (!saved.length) { savedResultsEl.textContent='Saxlanılan nəticə yoxdur'; return }
      savedResultsEl.innerHTML = saved.map(s=>`<div style='padding:8px;border-bottom:1px solid #f1f5f9'><strong>${s.title}</strong><div class='muted'>${s.correct} doğru · ${new Date(s.time).toLocaleString()}</div></div>`).join('')
    }

    // Bind UI
    function bindUI(){
      document.getElementById('open-random').onclick = ()=>{
        // start first non-premium test as quick demo
        const t = DB.tests.find(x=>!x.premium)
        if (t) startTest(t.id)
      }
      document.getElementById('next-q').onclick = nextQuestion
      document.getElementById('prev-q').onclick = prevQuestion
      document.getElementById('end-test').onclick = ()=>{ if (confirm('Testi bitirmək istəyirsən?')) endTest() }
      document.getElementById('retry').onclick = ()=>{ startTest(state.test.id) }
      document.getElementById('save-result').onclick = saveResult
      document.getElementById('buy-premium').onclick = ()=>{ buyPremium(); alert('Demo: premium aktivdir') }
      document.getElementById('quick-math').onclick = ()=>{ startTest('math-1') }
      document.getElementById('quick-az').onclick = ()=>{ startTest('aze-1') }
      document.getElementById('open-random').click()
    }

    // Init app
    init()
  </script>
</body>
</html>
