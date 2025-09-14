<template>
  <div class="about">
    <div class="content">
      <h1>🍅 About Pomodoro Timer</h1>
      <p>
        The Pomodoro Technique is a time management method developed by Francesco Cirillo in the
        late 1980s. It uses a timer to break down work into intervals, traditionally 25 minutes in
        length, separated by short breaks.
      </p>

      <h2>How it works:</h2>
      <ol>
        <li><strong>Focus:</strong> Work for 25 minutes with complete focus</li>
        <li><strong>Break:</strong> Take a 5-minute break</li>
        <li><strong>Repeat:</strong> Continue this cycle</li>
        <li><strong>Long Break:</strong> After 4 cycles, take a longer break (15-30 minutes)</li>
      </ol>

      <h2>Benefits:</h2>
      <ul>
        <li>Improved focus and concentration</li>
        <li>Better time management</li>
        <li>Reduced mental fatigue</li>
        <li>Increased productivity</li>
      </ul>

      <p class="tech-info">
        This app is built with <strong>Vue 3</strong>, <strong>TypeScript</strong>, and
        <strong>Vite</strong>. It demonstrates modern Vue development practices with composition API
        and TypeScript integration.
      </p>
    </div>
  </div>
</template>

<style scoped>
.about {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  line-height: 1.6;
}

.content {
  text-align: left;
}

h1 {
  color: #333;
  margin-bottom: 1.5rem;
  text-align: center;
}

h2 {
  color: #555;
  margin: 2rem 0 1rem 0;
  border-bottom: 2px solid #ff6b6b;
  padding-bottom: 0.5rem;
}

p {
  margin-bottom: 1rem;
  color: #666;
}

ol,
ul {
  margin: 1rem 0;
  padding-left: 2rem;
}

li {
  margin-bottom: 0.5rem;
  color: #666;
}

strong {
  color: #333;
}

.tech-info {
  background-color: #f8f9fa;
  border-left: 4px solid #ff6b6b;
  padding: 1rem;
  margin-top: 2rem;
  border-radius: 4px;
}

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
