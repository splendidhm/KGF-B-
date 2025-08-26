<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KG F&B - 제품 개발 프로세스 관리</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        /* 헤더 스타일 */
        .header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-symbol {
            width: 60px;
            height: 60px;
            position: relative;
        }

        .logo-symbol::before {
            content: '';
            position: absolute;
            top: 0;
            left: 20px;
            width: 0;
            height: 0;
            border-left: 15px solid transparent;
            border-right: 15px solid transparent;
            border-bottom: 25px solid #ff6b35;
            transform: rotate(45deg);
        }

        .logo-symbol::after {
            content: '';
            position: absolute;
            top: 15px;
            left: 15px;
            width: 0;
            height: 0;
            border-left: 12px solid transparent;
            border-right: 12px solid transparent;
            border-top: 20px solid #6a4c93;
        }

        .logo-symbol .bottom {
            position: absolute;
            bottom: 5px;
            left: 10px;
            width: 0;
            height: 0;
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-top: 18px solid #e91e63;
        }

        .logo-text {
            font-size: 28px;
            font-weight: bold;
            color: #6a4c93;
        }

        .header-info {
            text-align: right;
        }

        .header-info h2 {
            color: #6a4c93;
            margin-bottom: 5px;
        }

        .header-info p {
            color: #666;
            font-size: 14px;
        }

        /* 메인 콘텐츠 */
        .main-content {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 30px;
        }

        /* 사이드바 */
        .sidebar {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            height: fit-content;
        }

        .team-list {
            list-style: none;
        }

        .team-list li {
            margin-bottom: 15px;
        }

        .team-card {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 15px;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .team-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
        }

        .team-card.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        .team-card h3 {
            font-size: 16px;
            margin-bottom: 5px;
        }

        .team-card p {
            font-size: 12px;
            opacity: 0.9;
        }

        /* 프로세스 영역 */
        .process-area {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }

        .process-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }

        .process-title {
            font-size: 24px;
            color: #6a4c93;
            font-weight: bold;
        }

        .upload-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }

        .upload-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        /* 프로세스 단계 */
        .process-steps {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        .step-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            border-left: 5px solid #ddd;
            transition: all 0.3s ease;
            position: relative;
        }

        .step-card.completed {
            border-left-color: #4CAF50;
            background: linear-gradient(135deg, #e8f5e8 0%, #f1f8e9 100%);
        }

        .step-card.in-progress {
            border-left-color: #FF9800;
            background: linear-gradient(135deg, #fff3e0 0%, #ffe0b2 100%);
        }

        .step-card.pending {
            border-left-color: #9E9E9E;
            background: linear-gradient(135deg, #f5f5f5 0%, #eeeeee 100%);
        }

        .step-number {
            position: absolute;
            top: -10px;
            left: -10px;
            width: 30px;
            height: 30px;
            background: #6a4c93;
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 14px;
        }

        .step-title {
            font-size: 18px;
            font-weight: bold;
            color: #333;
            margin-bottom: 10px;
            margin-left: 20px;
        }

        .step-description {
            color: #666;
            font-size: 14px;
            margin-bottom: 15px;
            margin-left: 20px;
        }

        .step-status {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 12px;
            font-weight: bold;
            margin-left: 20px;
        }

        .status-completed {
            background: #4CAF50;
            color: white;
        }

        .status-in-progress {
            background: #FF9800;
            color: white;
        }

        .status-pending {
            background: #9E9E9E;
            color: white;
        }

        .step-team {
            margin-top: 10px;
            margin-left: 20px;
            font-size: 12px;
            color: #888;
        }

        /* 진행률 표시 */
        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 4px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4CAF50, #8BC34A);
            border-radius: 4px;
            transition: width 0.3s ease;
            width: 50%;
        }

        /* 반응형 디자인 */
        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .header {
                flex-direction: column;
                text-align: center;
                gap: 20px;
            }
            
            .process-steps {
                grid-template-columns: 1fr;
            }
        }

        /* 애니메이션 */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .step-card {
            animation: fadeInUp 0.6s ease forwards;
        }

        .step-card:nth-child(1) { animation-delay: 0.1s; }
        .step-card:nth-child(2) { animation-delay: 0.2s; }
        .step-card:nth-child(3) { animation-delay: 0.3s; }
        .step-card:nth-child(4) { animation-delay: 0.4s; }
        .step-card:nth-child(5) { animation-delay: 0.5s; }
        .step-card:nth-child(6) { animation-delay: 0.6s; }
    </style>
</head>
<body>
    <div class="container">
        <!-- 헤더 -->
        <header class="header">
            <div class="logo">
                <div class="logo-symbol">
                    <div class="bottom"></div>
                </div>
                <div class="logo-text">KG F&B</div>
            </div>
            <div class="header-info">
                <h2>제품 개발 프로세스 관리</h2>
                <p>육가공 제품 개발 및 출시 관리 시스템</p>
            </div>
        </header>

        <!-- 메인 콘텐츠 -->
        <div class="main-content">
            <!-- 사이드바 -->
            <aside class="sidebar">
                <h3 style="color: #6a4c93; margin-bottom: 20px; font-size: 18px;">참여 부서</h3>
                <ul class="team-list">
                    <li>
                        <div class="team-card active">
                            <h3>사업팀 (영업팀)</h3>
                            <p>제품 개발 의뢰 및 요구사항 정의</p>
                        </div>
                    </li>
                    <li>
                        <div class="team-card">
                            <h3>R&D팀</h3>
                            <p>제품 개발 및 원재료 서치</p>
                        </div>
                    </li>
                    <li>
                        <div class="team-card">
                            <h3>구매팀</h3>
                            <p>자재 입고 및 공급업체 관리</p>
                        </div>
                    </li>
                    <li>
                        <div class="team-card">
                            <h3>품질팀</h3>
                            <p>품질 관리 및 표시사항 준비</p>
                        </div>
                    </li>
                    <li>
                        <div class="team-card">
                            <h3>생산팀</h3>
                            <p>생산 계획 및 제조 관리</p>
                        </div>
                    </li>
                    <li>
                        <div class="team-card">
                            <h3>물류팀</h3>
                            <p>출고 및 배송 관리</p>
                        </div>
                    </li>
                </ul>
            </aside>

            <!-- 프로세스 영역 -->
            <main class="process-area">
                <div class="process-header">
                    <h2 class="process-title">제품 개발 프로세스</h2>
                    <button class="upload-btn">+ 새 프로젝트 등록</button>
                </div>

                <!-- 진행률 -->
                <div class="progress-bar">
                    <div class="progress-fill"></div>
                </div>

                <!-- 프로세스 단계 -->
                <div class="process-steps">
                    <div class="step-card completed">
                        <div class="step-number">1</div>
                        <h3 class="step-title">제품 개발 의뢰</h3>
                        <p class="step-description">사업팀에서 새로운 제품 개발 요청을 업로드하고 요구사항을 정의합니다.</p>
                        <span class="step-status status-completed">완료</span>
                        <div class="step-team">담당: 사업팀 (영업팀)</div>
                    </div>

                    <div class="step-card in-progress">
                        <div class="step-number">2</div>
                        <h3 class="step-title">R&D 접수 및 원재료 서치</h3>
                        <p class="step-description">R&D팀에서 제품 개발에 필요한 원재료를 조사하고 기술적 검토를 진행합니다.</p>
                        <span class="step-status status-in-progress">진행중</span>
                        <div class="step-team">담당: R&D팀</div>
                    </div>

                    <div class="step-card pending">
                        <div class="step-number">3</div>
                        <h3 class="step-title">구매팀 자재 준비</h3>
                        <p class="step-description">구매팀에서 해당 자재의 입고 가능 여부를 확인하고 공급업체와 계약을 진행합니다.</p>
                        <span class="step-status status-pending">대기중</span>
                        <div class="step-team">담당: 구매팀</div>
                    </div>

                    <div class="step-card pending">
                        <div class="step-number">4</div>
                        <h3 class="step-title">품질팀 표시사항 준비</h3>
                        <p class="step-description">품질팀에서 제품의 표시사항을 준비하고 품질 관련 업무를 수행합니다.</p>
                        <span class="step-status status-pending">대기중</span>
                        <div class="step-team">담당: 품질팀</div>
                    </div>

                    <div class="step-card pending">
                        <div class="step-number">5</div>
                        <h3 class="step-title">생산 계획 수립</h3>
                        <p class="step-description">생산팀에서 제품 생산 계획을 수립하고 생산 일정을 관리합니다.</p>
                        <span class="step-status status-pending">대기중</span>
                        <div class="step-team">담당: 생산팀</div>
                    </div>

                    <div class="step-card pending">
                        <div class="step-number">6</div>
                        <h3 class="step-title">출고 및 배송</h3>
                        <p class="step-description">물류팀에서 완성된 제품의 출고 및 배송을 관리합니다.</p>
                        <span class="step-status status-pending">대기중</span>
                        <div class="step-team">담당: 물류팀</div>
                    </div>
                </div>
            </main>
        </div>
    </div>

    <script>
        // 팀 카드 클릭 이벤트
        document.querySelectorAll('.team-card').forEach(card => {
            card.addEventListener('click', function() {
                // 모든 카드에서 active 클래스 제거
                document.querySelectorAll('.team-card').forEach(c => c.classList.remove('active'));
                // 클릭된 카드에 active 클래스 추가
                this.classList.add('active');
            });
        });

        // 진행률 애니메이션
        setTimeout(() => {
            const progressFill = document.querySelector('.progress-fill');
            progressFill.style.width = '33%'; // 2단계까지 완료된 상태
        }, 1000);

        // 새 프로젝트 등록 버튼 클릭 이벤트
        document.querySelector('.upload-btn').addEventListener('click', function() {
            alert('새 프로젝트 등록 기능이 실행됩니다.\n\n이 기능은 실제 구현 시 제품 개발 의뢰서 업로드 및\n프로젝트 정보 입력 폼을 제공합니다.');
        });
    </script>
</body>
</html>
