# NC-AI-internship
backup of NC-AI internship

## Internship info
- 기업: NC AI
- 근무 기간: 2025.03 - 2025.08
- 부서: 그래픽스 AI lab 모션서비스실 Facial animation 팀
- 업무: 발화 기반 얼굴 애니메이션 생성 모델 성능 개선

## Face Animator Model

https://github.com/user-attachments/assets/9c899540-1f0d-443a-b29a-c78b2a400c7e

- 발화 audio를 기반으로, 알맞은 lipsync와 얼굴 표정을 보여주는 3D facial animation 생성 모델
- 다양한 발화자 기반 얼굴 애니메이션 생성
- 얼굴 표정에 반영되는 감정을 사용자가 자유롭게 선택 가능
- 시간에 따른 자연스러운 감정 변화가 가능하며, 사용자가 감정 및 변화 타이밍 조절 가능

<img width="755" height="311" alt="image" src="https://github.com/user-attachments/assets/4a8af5ac-68cc-4d37-87d3-c2067ad2cb2e" />

- transformer 기반의 diffusion model 이용
- 자연스러운 얼굴 애니메이션을 위해서는 일관되지 않고 불규칙적인 얼굴 표현이 필요, 입력에 대해 다양한 결과를 생성할 수 있는 diffusion model의 특성이 적합하다고 판단하여 채택
-  input: 발화 audio, conditions (발화자 id, emotion)
-  output: frame 별 ARKit blendshape weight value
-  입력으로 주어진 음성은 pre-trained audio encoder를 통과한 후, cross attention에 반영됨
-  발화자, 감정, diffusion timestep 정보는 embedding을 거친 후, attention의 key와 value 값으로 들어감
-  GT animation(blendshape weight)에 대한 reconstruction loss와 함께 jittering을 줄이고자 velocity loss 사용
