<template>
  <div class="landing">
    <HeroSection />
    <AboutSection id="about" />
    <SkillsSection id="skills" />
    <!-- <ProjectsSection /> -->
    <ReviewSection id="review" />
    <MentorBenefits id="benefits" />
    <ContactSection />
  </div>
</template>

<style scoped>
.landing {
  /* background: linear-gradient( */
  /*   to bottom, */
  /*   #333 0%, */
  /*   #f94d6a 12.5%, */
  /*   #ff7f50 25%, */
  /*   #f9c80e 37.5%, */
  /*   #43e97b 50%, */
  /*   #38f9d7 62.5%, */
  /*   #4facfe 75%, */
  /*   #6a82fb 100% */
  /* ); */

  /* background: linear-gradient( */
  /*   to bottom, */
  /*   #ff6b6b 0%, */
  /*   #ff6b6b 10%, */
  /*   transparent 20%, */
  /*   #f9c80e 30%, */
  /*   #f9c80e 40%, */
  /*   transparent 50%, */
  /*   #43e97b 60%, */
  /*   #43e97b 70%, */
  /*   transparent 80%, */
  /*   #4facfe 90%, */
  /*   #4facfe 100% */
  /* ); */

  background: linear-gradient(
    to bottom,
    #1e1e1e 0%,
    #1e1e1e 10%,
    #5c258d 25%,
    #4389a2 40%,
    #56ab2f 55%,
    #f9c80e 70%,
    #f78ca0 85%,
    #fbc2eb 100%
  );

  background: linear-gradient(
    to bottom,
    #1e1e1e 0%,
    #1e1e1e 10%,
    #3a3a52 25%,
    #4e4376 40%,
    #6e44ff 55%,
    #44b09e 70%,
    #b8c6db 85%,
    #f5f7fa 100%
  );

  background: linear-gradient(
    to bottom,
    #1e1e1e 0%,
    #1e1e1e 10%,
    #5c258d 25%,
    #4389a2 40%,
    #56ab2f 55%,
    #f9c80e 70%,
    #feb47b 85%,
    #ffffff 100%
  );

  background: linear-gradient(
    to bottom,
    #1e1e1e 0%,
    #2c3e50 15%,
    /* глубокий графитовый синий */ #34495e 30%,
    /* насыщенный серо-синий */ #264653 50%,
    /* глубокий тёмный teal */ #3a5a40 65%,
    /* благородный зелёный */ #6c4f3d 80%,
    /* тёплый коричнево-золотой */ #d4af37 95% /* элегантное золото */
  );

  background: linear-gradient(
    to bottom,
    #1e1e1e 0%,
    #2c3e50 15%,
    /* глубокий графитовый синий */ #34495e 30%,
    /* насыщенный серо-синий */ #264653 50%,
    /* глубокий тёмный teal */ #3a5a40 65%,
    /* благородный зелёный */ #3c3c52 80%,
    /* тёмно-серый с фиолетовым подтоном */ #d4af37 95% /* элегантное золото */
  );

  background: linear-gradient(
    to bottom,
    #1e1e1e 0%,
    /* глубокий тёмно-серый */ #2c3e50 15%,
    /* графитовый синий */ #34495e 30%,
    /* серо-синий */ #264653 45%,
    /* тёмный teal */ #3a5a40 60%,
    /* холодный зелёный */ #3c3c52 75%,
    /* фиолетово-серый */ #2a3b8d 90%,
    /* благородный тёмно-синий */ #1a2a6c 100% /* глубокий синий индиго */
  );
}
</style>
