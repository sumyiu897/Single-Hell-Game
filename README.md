<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>單身即地獄 · 終極完整版</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
        }
        body {
            min-height: 100vh;
            background: #f5efe8;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 10px;
            overflow: hidden;
            height: 100vh;
        }
        .app {
            max-width: 650px;
            width: 100%;
            height: 95vh;
            max-height: 820px;
            background: #ffffff;
            border-radius: 36px;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.06);
            border: 1px solid #f0e8e0;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            position: relative;
        }
        .turn-display {
            position: absolute;
            top: 12px;
            left: 16px;
            background: #e8ddd2;
            padding: 4px 14px;
            border-radius: 40px;
            font-size: 0.75rem;
            font-weight: 700;
            color: #3d2c24;
            z-index: 5;
            border: 1px solid #d5c4b6;
            pointer-events: none;
        }
        .swipe-container {
            display: flex;
            flex: 1;
            overflow-x: auto;
            overflow-y: hidden;
            scroll-snap-type: x mandatory;
            -webkit-overflow-scrolling: touch;
            scroll-behavior: smooth;
            touch-action: pan-x;
            cursor: grab;
        }
        .swipe-container:active {
            cursor: grabbing;
        }
        .swipe-container::-webkit-scrollbar {
            display: none;
        }
        .page-slide {
            flex: 0 0 100%;
            scroll-snap-align: start;
            overflow-y: auto;
            padding: 14px;
            height: 100%;
            background: #ffffff;
        }
        .page-slide::-webkit-scrollbar {
            width: 3px;
        }
        .page-slide::-webkit-scrollbar-thumb {
            background: #d5c4b6;
            border-radius: 10px;
        }
        .swipe-nav {
            display: flex;
            justify-content: center;
            gap: 12px;
            padding: 8px 0 10px;
            flex-shrink: 0;
            background: #ffffff;
            border-top: 1px solid #f0e8e0;
            transition: opacity 0.3s ease;
        }
        .swipe-nav.hidden {
            display: none;
        }
        .swipe-nav button {
            background: none;
            border: none;
            color: #b8a092;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            padding: 6px 20px;
            border-radius: 40px;
            transition: 0.2s;
        }
        .swipe-nav button.active {
            background: #e8ddd2;
            color: #3d2c24;
        }
        .swipe-nav button:active {
            transform: scale(0.95);
        }

        .header {
            text-align: center;
            padding-bottom: 10px;
            border-bottom: 2px solid #f0e6dc;
            margin-bottom: 12px;
            margin-top: 4px;
        }
        .header h1 {
            font-size: 1.5rem;
            font-weight: 700;
            color: #3d2c24;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            flex-wrap: wrap;
        }
        .header h1 small {
            font-size: 0.65rem;
            background: #f5ede6;
            padding: 2px 12px;
            border-radius: 40px;
            color: #9a7a6a;
            border: 1px solid #e8dcd2;
        }
        .sub {
            color: #b09585;
            font-size: 0.75rem;
            margin-top: 2px;
        }

        .stamina-bar {
            display: flex;
            align-items: center;
            gap: 8px;
            background: #faf6f2;
            padding: 6px 12px;
            border-radius: 50px;
            border: 1px solid #ede4db;
            margin-bottom: 8px;
        }
        .stamina-bar .label {
            font-size: 0.7rem;
            font-weight: 600;
            color: #6b5a4e;
            white-space: nowrap;
        }
        .stamina-bar .track {
            flex: 1;
            height: 8px;
            background: #ede4db;
            border-radius: 20px;
            overflow: hidden;
        }
        .stamina-bar .fill {
            height: 100%;
            background: linear-gradient(90deg, #e88a7a, #d97d4a);
            border-radius: 20px;
            transition: width 0.3s;
        }
        .stamina-bar .value {
            font-size: 0.7rem;
            font-weight: 700;
            color: #3d2c24;
            min-width: 30px;
            text-align: right;
        }

        .status-bar {
            display: flex;
            justify-content: space-around;
            background: #faf6f2;
            padding: 6px 10px;
            border-radius: 50px;
            border: 1px solid #ede4db;
            margin-bottom: 10px;
            flex-wrap: wrap;
            gap: 4px;
        }
        .status-item {
            display: flex;
            align-items: center;
            gap: 4px;
            color: #6b5a4e;
            font-weight: 500;
            font-size: 0.75rem;
        }
        .status-item .num {
            background: #ede4db;
            padding: 0 10px;
            border-radius: 30px;
            color: #3d2c24;
            font-weight: 700;
            border: 1px solid #e0d3c8;
        }

        .player-section {
            background: #faf6f2;
            border-radius: 30px;
            padding: 8px 10px;
            margin-bottom: 10px;
            border: 1px solid #ede4db;
        }
        .player-select {
            display: flex;
            flex-wrap: wrap;
            gap: 4px;
            justify-content: center;
            margin: 4px 0;
            min-height: 32px;
        }
        .player-select .btn {
            padding: 4px 10px;
            font-size: 0.7rem;
            background: #ffffff;
            border: 1px solid #e0d3c8;
            border-radius: 40px;
            color: #6b5a4e;
            cursor: pointer;
            transition: 0.2s;
        }
        .player-select .btn.player-active {
            background: #dccfc4;
            border-color: #b8a092;
            font-weight: 700;
        }

        .roster {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-bottom: 10px;
        }
        .gender-group {
            background: #faf6f2;
            border-radius: 30px;
            padding: 8px 10px;
            border: 1px solid #ede4db;
        }
        .gender-label {
            color: #9a7a6a;
            font-weight: 600;
            font-size: 0.75rem;
            padding-bottom: 4px;
            border-bottom: 1px solid #ede4db;
            margin-bottom: 6px;
            display: flex;
            justify-content: space-between;
        }
        .avatar-list {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
        }
        .avatar {
            background: #ffffff;
            border-radius: 40px;
            padding: 5px 12px;
            border: 1px solid #e0d3c8;
            color: #4d3a2e;
            font-size: 0.75rem;
            display: inline-flex;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            transition: 0.15s;
            touch-action: manipulation;
        }
        .avatar:active {
            transform: scale(0.95);
        }
        .avatar.paired {
            background: #f0e8e0;
            border-color: #d5c4b6;
            opacity: 0.6;
            cursor: not-allowed;
        }
        .avatar.player {
            border-color: #b8a092;
            background: #e8ddd2;
        }
        .avatar .badge {
            font-size: 0.45rem;
            background: #b8a092;
            color: #fff;
            padding: 0 5px;
            border-radius: 20px;
        }
        .avatar .heart-icon {
            color: #e88a7a;
            font-size: 0.65rem;
        }
        .avatar .suspicion {
            color: #b8a092;
            font-size: 0.6rem;
            margin-left: 2px;
            cursor: help;
        }

        .interact-modal {
            display: none;
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: #ffffff;
            border-radius: 32px 32px 0 0;
            padding: 20px 18px 24px;
            box-shadow: 0 -8px 30px rgba(0, 0, 0, 0.08);
            z-index: 30;
            border-top: 1px solid #f0e8e0;
        }
        .interact-modal.open {
            display: block;
        }
        .interact-modal .modal-title {
            font-weight: 700;
            color: #3d2c24;
            font-size: 1rem;
            text-align: center;
            margin-bottom: 12px;
        }
        .interact-modal .modal-sub {
            color: #9a7a6a;
            font-size: 0.8rem;
            text-align: center;
            margin-bottom: 14px;
        }
        .interact-modal .modal-actions {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
        }
        .interact-modal .modal-actions button {
            padding: 10px 8px;
            border: 1px solid #e0d3c8;
            border-radius: 40px;
            background: #ffffff;
            font-weight: 600;
            color: #4d3a2e;
            cursor: pointer;
            font-size: 0.8rem;
            transition: 0.15s;
        }
        .interact-modal .modal-actions button:active {
            transform: scale(0.95);
        }
        .interact-modal .modal-actions .btn-primary {
            background: #e8ddd2;
            border-color: #d5c4b6;
        }
        .interact-modal .modal-actions .btn-heart {
            background: #fce8e0;
            border-color: #eaccc0;
            color: #7a4a3a;
        }
        .interact-modal .modal-actions .btn-light {
            background: #f5efe8;
        }
        .interact-modal .modal-actions .btn-info {
            background: #dde4e8;
            border-color: #c5d0d4;
            color: #3d4a4e;
        }
        .interact-modal .modal-close {
            display: block;
            width: 100%;
            margin-top: 10px;
            padding: 8px;
            border: none;
            background: none;
            color: #b8a092;
            font-size: 0.75rem;
            cursor: pointer;
        }

        .rest-area {
            display: flex;
            justify-content: center;
            margin: 8px 0 4px;
            gap: 8px;
            flex-wrap: wrap;
        }
        .rest-btn {
            background: #e8ddd2;
            border: 1px solid #d5c4b6;
            border-radius: 40px;
            padding: 8px 32px;
            font-weight: 700;
            color: #3d2c24;
            font-size: 0.9rem;
            cursor: pointer;
            transition: 0.15s;
            flex: 1;
            min-width: 100px;
        }
        .rest-btn:active {
            transform: scale(0.96);
        }
        .rest-btn:disabled {
            opacity: 0.4;
            cursor: not-allowed;
        }

        .log-area {
            background: #faf6f2;
            border-radius: 30px;
            padding: 8px 12px;
            border: 1px solid #ede4db;
            min-height: 50px;
            max-height: 80px;
            overflow-y: auto;
            margin-top: 8px;
        }
        .log-line {
            border-left: 3px solid #d5c4b6;
            padding-left: 8px;
            margin: 2px 0;
            color: #6b5a4e;
            font-size: 0.75rem;
            line-height: 1.3;
        }
        .log-line strong {
            color: #3d2c24;
        }

        .btn-sm {
            padding: 3px 10px;
            font-size: 0.65rem;
            background: #f5efe8;
            border: 1px solid #e0d3c8;
            color: #9a7a6a;
            border-radius: 40px;
            cursor: pointer;
        }
        .btn-sm:active {
            transform: scale(0.95);
        }
        .log-toolbar {
            display: flex;
            justify-content: flex-end;
            gap: 6px;
            margin-top: 4px;
        }

        .phone-header {
            display: flex;
            align-items: center;
            gap: 10px;
            padding-bottom: 10px;
            border-bottom: 2px solid #f0e6dc;
            margin-bottom: 10px;
        }
        .phone-header h2 {
            font-size: 1.1rem;
            color: #3d2c24;
            font-weight: 600;
        }
        .phone-header .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #4caf50;
            margin-left: auto;
        }
        .tab-btn-phone {
            flex: 1;
            padding: 6px;
            border: none;
            border-radius: 40px;
            background: transparent;
            font-weight: 600;
            color: #9a7a6a;
            cursor: pointer;
            font-size: 0.75rem;
            transition: 0.2s;
        }
        .tab-btn-phone.active {
            background: #ffffff;
            color: #3d2c24;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
        }
        .chat-list {
            display: flex;
            flex-direction: column;
            gap: 6px;
            margin-bottom: 10px;
        }
        .chat-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px 12px;
            background: #faf6f2;
            border-radius: 20px;
            border: 1px solid #ede4db;
            cursor: pointer;
            transition: 0.15s;
        }
        .chat-item:active {
            transform: scale(0.97);
        }
        .chat-item .avatar-chat {
            width: 38px;
            height: 38px;
            border-radius: 50%;
            background: #e8ddd2;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            flex-shrink: 0;
        }
        .chat-item .info {
            flex: 1;
            min-width: 0;
        }
        .chat-item .info .name {
            font-weight: 600;
            color: #3d2c24;
            font-size: 0.85rem;
        }
        .chat-item .info .last-msg {
            color: #9a7a6a;
            font-size: 0.7rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .chat-item .info .time {
            font-size: 0.6rem;
            color: #b8a092;
        }
        .chat-item .info .affection {
            font-size: 0.6rem;
            color: #e88a7a;
            margin-left: 4px;
        }

        .chat-window {
            display: none;
            flex-direction: column;
            height: 100%;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: #ffffff;
            z-index: 25;
            padding: 14px;
            border-radius: 36px;
            overflow: hidden;
        }
        .chat-window.open {
            display: flex;
        }
        .chat-header {
            display: flex;
            align-items: center;
            gap: 10px;
            padding-bottom: 10px;
            border-bottom: 2px solid #f0e6dc;
            flex-shrink: 0;
        }
        .chat-header .back {
            font-size: 1.4rem;
            cursor: pointer;
            padding: 2px 6px;
            border: none;
            background: none;
            color: #6b5a4e;
            z-index: 26;
            position: relative;
        }
        .chat-header .back:active {
            transform: scale(0.9);
        }
        .chat-header .name {
            font-weight: 600;
            color: #3d2c24;
            font-size: 0.95rem;
        }
        .chat-header .status-text {
            font-size: 0.65rem;
            color: #9a7a6a;
            margin-left: auto;
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 10px 0;
            display: flex;
            flex-direction: column;
            gap: 6px;
            -webkit-overflow-scrolling: touch;
        }
        .chat-messages .msg {
            max-width: 80%;
            padding: 8px 14px;
            border-radius: 20px;
            font-size: 0.82rem;
            line-height: 1.4;
            word-break: break-word;
        }
        .chat-messages .msg.sent {
            align-self: flex-end;
            background: #e8ddd2;
            color: #3d2c24;
            border-bottom-right-radius: 4px;
        }
        .chat-messages .msg.received {
            align-self: flex-start;
            background: #f5efe8;
            color: #3d2c24;
            border-bottom-left-radius: 4px;
        }
        .chat-messages .msg .time-tag {
            font-size: 0.5rem;
            color: #b8a092;
            margin-top: 2px;
            display: block;
            text-align: right;
        }
        .chat-messages .typing-indicator {
            align-self: flex-start;
            background: #f5efe8;
            padding: 8px 14px;
            border-radius: 20px;
            border-bottom-left-radius: 4px;
            font-size: 0.8rem;
            color: #9a7a6a;
        }
        .chat-messages .typing-indicator .dot {
            display: inline-block;
            animation: typing 1.4s infinite;
        }
        .chat-messages .typing-indicator .dot:nth-child(2) {
            animation-delay: 0.2s;
        }
        .chat-messages .typing-indicator .dot:nth-child(3) {
            animation-delay: 0.4s;
        }
        @keyframes typing {
            0%,
            60%,
            100% {
                opacity: 0.3;
                transform: translateY(0);
            }
            30% {
                opacity: 1;
                transform: translateY(-4px);
            }
        }

        .chat-input-area {
            display: flex;
            gap: 6px;
            padding: 10px 0 4px;
            border-top: 1px solid #f0e8e0;
            flex-shrink: 0;
            background: #ffffff;
            position: sticky;
            bottom: 0;
        }
        .chat-input-area input {
            flex: 1;
            padding: 10px 14px;
            border: 1px solid #e0d3c8;
            border-radius: 30px;
            font-size: 0.85rem;
            outline: none;
            background: #faf6f2;
            color: #3d2c24;
            min-height: 44px;
        }
        .chat-input-area input:focus {
            border-color: #b8a092;
        }
        .chat-input-area .send-btn {
            padding: 10px 18px;
            background: #e8ddd2;
            border: none;
            border-radius: 30px;
            font-weight: 600;
            color: #3d2c24;
            cursor: pointer;
            font-size: 0.85rem;
            min-height: 44px;
            min-width: 60px;
        }
        .chat-input-area .send-btn:active {
            transform: scale(0.95);
        }

        .ig-profile {
            text-align: center;
            padding: 6px 0 10px;
            border-bottom: 1px solid #f0e8e0;
            margin-bottom: 10px;
        }
        .ig-profile .ig-avatar {
            width: 64px;
            height: 64px;
            border-radius: 50%;
            background: #e8ddd2;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            margin: 0 auto 4px;
            border: 3px solid #dccfc4;
        }
        .ig-profile .ig-name {
            font-weight: 700;
            color: #3d2c24;
            font-size: 0.95rem;
        }
        .ig-profile .ig-bio {
            color: #9a7a6a;
            font-size: 0.75rem;
            margin: 2px 0;
        }
        .ig-profile .ig-stats {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 4px;
        }
        .ig-profile .ig-stats span {
            font-size: 0.7rem;
            color: #6b5a4e;
        }
        .ig-profile .ig-stats strong {
            color: #3d2c24;
            display: block;
            font-size: 0.85rem;
        }

        .ig-post-area {
            background: #faf6f2;
            border-radius: 24px;
            padding: 12px 14px;
            border: 1px solid #ede4db;
            margin-bottom: 12px;
        }
        .ig-post-area textarea {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid #e0d3c8;
            border-radius: 20px;
            font-size: 0.8rem;
            outline: none;
            resize: none;
            background: #ffffff;
            color: #3d2c24;
            font-family: inherit;
            min-height: 60px;
        }
        .ig-post-area textarea:focus {
            border-color: #b8a092;
        }
        .ig-post-area .post-btn-row {
            display: flex;
            gap: 8px;
            margin-top: 8px;
            justify-content: flex-end;
        }
        .ig-post-area .post-btn-row button {
            padding: 6px 18px;
            border: 1px solid #e0d3c8;
            border-radius: 40px;
            background: #ffffff;
            font-weight: 600;
            color: #4d3a2e;
            cursor: pointer;
            font-size: 0.75rem;
            transition: 0.15s;
        }
        .ig-post-area .post-btn-row button:active {
            transform: scale(0.95);
        }
        .ig-post-area .post-btn-row .btn-primary {
            background: #e8ddd2;
            border-color: #d5c4b6;
        }

        .ig-posts {
            display: flex;
            flex-direction: column;
            gap: 10px;
            padding-bottom: 8px;
        }
        .ig-post {
            background: #faf6f2;
            border-radius: 20px;
            padding: 10px 12px;
            border: 1px solid #ede4db;
        }
        .ig-post .post-header {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 4px;
        }
        .ig-post .post-header .post-avatar {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            background: #e8ddd2;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
        }
        .ig-post .post-header .post-name {
            font-weight: 600;
            color: #3d2c24;
            font-size: 0.75rem;
            cursor: pointer;
        }
        .ig-post .post-header .post-name:active {
            opacity: 0.6;
        }
        .ig-post .post-header .post-time {
            font-size: 0.6rem;
            color: #b8a092;
            margin-left: auto;
        }
        .ig-post .post-content {
            color: #4d3a2e;
            font-size: 0.8rem;
            line-height: 1.4;
            padding: 2px 0;
        }
        .ig-post .post-actions {
            display: flex;
            gap: 16px;
            margin-top: 6px;
            font-size: 0.7rem;
            color: #9a7a6a;
        }
        .ig-post .post-actions button {
            background: none;
            border: none;
            color: #9a7a6a;
            font-size: 0.7rem;
            cursor: pointer;
            padding: 2px 6px;
            border-radius: 20px;
            transition: 0.15s;
        }
        .ig-post .post-actions button:active {
            transform: scale(0.9);
        }
        .ig-post .post-actions .liked {
            color: #e88a7a;
            font-weight: 700;
        }
        .ig-post .comment-area {
            margin-top: 6px;
            display: flex;
            gap: 6px;
        }
        .ig-post .comment-area input {
            flex: 1;
            padding: 4px 10px;
            border: 1px solid #e0d3c8;
            border-radius: 30px;
            font-size: 0.7rem;
            outline: none;
            background: #ffffff;
        }
        .ig-post .comment-area input:focus {
            border-color: #b8a092;
        }
        .ig-post .comment-area button {
            padding: 4px 12px;
            border: none;
            border-radius: 30px;
            background: #e8ddd2;
            font-size: 0.65rem;
            font-weight: 600;
            color: #3d2c24;
            cursor: pointer;
        }
        .ig-post .comment-area button:active {
            transform: scale(0.95);
        }
        .ig-post .comments {
            margin-top: 4px;
            font-size: 0.7rem;
            color: #6b5a4e;
        }
        .ig-post .comments .comment {
            padding: 2px 0;
            border-bottom: 1px solid #ede4db;
        }
        .ig-post .comments .comment strong {
            color: #3d2c24;
        }
        .ig-post .post-header .post-name .mine {
            font-size: 0.5rem;
            background: #e8ddd2;
            padding: 0 6px;
            border-radius: 20px;
            color: #9a7a6a;
            margin-left: 4px;
        }

        .my-profile {
            text-align: center;
            padding: 8px 0 12px;
        }
        .my-profile .my-avatar-wrapper {
            position: relative;
            display: inline-block;
        }
        .my-profile .my-avatar {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: #e8ddd2;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.8rem;
            margin: 0 auto 8px;
            border: 4px solid #dccfc4;
            cursor: pointer;
            transition: 0.15s;
            overflow: hidden;
        }
        .my-profile .my-avatar:active {
            transform: scale(0.95);
        }
        .my-profile .my-avatar img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .my-profile .edit-hint {
            display: block;
            font-size: 0.5rem;
            color: #b8a092;
            margin-top: -4px;
            margin-bottom: 6px;
        }
        .my-profile .my-name {
            font-size: 1.2rem;
            font-weight: 700;
            color: #3d2c24;
        }
        .my-profile .my-status {
            color: #9a7a6a;
            font-size: 0.85rem;
            margin-top: 2px;
        }

        .my-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 12px 0;
        }
        .my-stat-card {
            background: #faf6f2;
            border-radius: 24px;
            padding: 14px 12px;
            border: 1px solid #ede4db;
            text-align: center;
        }
        .my-stat-card .stat-icon {
            font-size: 1.5rem;
        }
        .my-stat-card .stat-value {
            font-size: 1.3rem;
            font-weight: 800;
            color: #3d2c24;
            margin-top: 2px;
        }
        .my-stat-card .stat-label {
            font-size: 0.7rem;
            color: #9a7a6a;
        }

        .my-partner {
            background: #faf6f2;
            border-radius: 24px;
            padding: 14px 16px;
            border: 1px solid #ede4db;
            margin: 8px 0 12px;
            text-align: center;
        }
        .my-partner .partner-label {
            font-size: 0.7rem;
            color: #9a7a6a;
            font-weight: 600;
        }
        .my-partner .partner-name {
            font-size: 1.1rem;
            font-weight: 700;
            color: #3d2c24;
            margin-top: 2px;
        }
        .my-partner .partner-empty {
            color: #b8a092;
            font-size: 0.9rem;
        }

        .my-actions {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
            margin-top: 8px;
        }
        .my-actions button {
            flex: 1;
            min-width: 80px;
            padding: 10px 12px;
            border: 1px solid #e0d3c8;
            border-radius: 40px;
            background: #ffffff;
            font-weight: 600;
            color: #4d3a2e;
            cursor: pointer;
            font-size: 0.8rem;
            transition: 0.15s;
        }
        .my-actions button:active {
            transform: scale(0.95);
        }
        .my-actions .btn-primary {
            background: #e8ddd2;
            border-color: #d5c4b6;
        }

        /* 成就列表 */
        .achievement-list {
            background: #faf6f2;
            border-radius: 20px;
            padding: 10px 14px;
            border: 1px solid #ede4db;
            margin-top: 12px;
        }
        .achievement-list .ach-title {
            font-size: 0.7rem;
            color: #9a7a6a;
            font-weight: 600;
            margin-bottom: 4px;
        }
        .achievement-list .ach-item {
            font-size: 0.75rem;
            color: #6b5a4e;
            padding: 2px 0;
        }

        .rank-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 14px;
            border-bottom: 1px solid #ede4db;
            align-items: center;
        }
        .rank-item .rank {
            font-weight: 700;
            color: #b8a092;
            width: 30px;
        }
        .rank-item .rank.gold {
            color: #ffd700;
        }
        .rank-item .rank.silver {
            color: #c0c0c0;
        }
        .rank-item .rank.bronze {
            color: #cd7f32;
        }
        .rank-item .name {
            flex: 1;
            font-weight: 500;
            color: #3d2c24;
        }
        .rank-item .aff {
            font-weight: 600;
            color: #e88a7a;
        }

        .story-overlay {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(6px);
            z-index: 40;
            border-radius: 36px;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            padding: 24px;
        }
        .story-overlay.open {
            display: flex;
        }
        .story-box {
            background: #ffffff;
            border-radius: 32px;
            padding: 28px 24px;
            max-width: 450px;
            width: 100%;
            max-height: 80vh;
            overflow-y: auto;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            animation: popIn 0.4s ease;
        }
        .story-box .story-header {
            display: flex;
            align-items: center;
            gap: 12px;
            border-bottom: 2px solid #f0e6dc;
            padding-bottom: 12px;
            margin-bottom: 14px;
        }
        .story-box .story-header .story-avatar {
            font-size: 2.2rem;
        }
        .story-box .story-header .story-name {
            font-size: 1.1rem;
            font-weight: 700;
            color: #3d2c24;
        }
        .story-box .story-header .story-chapter {
            font-size: 0.7rem;
            color: #b8a092;
            margin-left: auto;
            background: #f5efe8;
            padding: 2px 12px;
            border-radius: 20px;
        }
        .story-box .story-dialogue {
            font-size: 0.95rem;
            line-height: 1.7;
            color: #4d3a2e;
            padding: 8px 0 14px;
            white-space: pre-line;
            min-height: 80px;
        }
        .story-box .story-choices {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-top: 10px;
        }
        .story-box .story-choices button {
            padding: 10px 16px;
            border: 1px solid #e0d3c8;
            border-radius: 40px;
            background: #ffffff;
            font-weight: 600;
            color: #4d3a2e;
            cursor: pointer;
            font-size: 0.85rem;
            transition: 0.15s;
            text-align: left;
        }
        .story-box .story-choices button:active {
            transform: scale(0.97);
        }
        .story-box .story-choices button:hover {
            background: #f5efe8;
        }
        .story-box .story-choices button .choice-tag {
            font-size: 0.6rem;
            color: #b8a092;
            margin-right: 6px;
        }
        .story-box .story-result {
            margin-top: 12px;
            padding: 12px 16px;
            border-radius: 20px;
            background: #faf6f2;
            font-size: 0.85rem;
            color: #6b5a4e;
            text-align: center;
            border: 1px solid #ede4db;
            display: none;
        }
        .story-box .story-result.show {
            display: block;
        }
        .story-box .story-skip {
            display: block;
            width: 100%;
            margin-top: 12px;
            padding: 8px;
            border: none;
            background: none;
            color: #b8a092;
            font-size: 0.75rem;
            cursor: pointer;
            text-align: center;
        }
        .story-box .story-skip:active {
            opacity: 0.6;
        }

        .achievement-toast {
            position: absolute;
            top: 60px;
            left: 50%;
            transform: translateX(-50%);
            background: #e8ddd2;
            padding: 10px 20px;
            border-radius: 40px;
            border: 1px solid #d5c4b6;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
            z-index: 45;
            font-weight: 600;
            font-size: 0.85rem;
            color: #3d2c24;
            display: none;
            animation: slideDown 0.4s ease;
            max-width: 90%;
        }
        .achievement-toast.show {
            display: block;
        }
        @keyframes slideDown {
            0% {
                opacity: 0;
                transform: translateX(-50%) translateY(-20px);
            }
            100% {
                opacity: 1;
                transform: translateX(-50%) translateY(0);
            }
        }
        @keyframes popIn {
            0% {
                transform: scale(0.9);
                opacity: 0;
            }
            100% {
                transform: scale(1);
                opacity: 1;
            }
        }

        .event-notification {
            position: absolute;
            top: 60px;
            left: 50%;
            transform: translateX(-50%);
            background: #fce8e0;
            padding: 12px 24px;
            border-radius: 40px;
            border: 2px solid #eaccc0;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
            z-index: 42;
            font-weight: 600;
            font-size: 0.85rem;
            color: #7a4a3a;
            display: none;
            animation: slideDown 0.4s ease;
            text-align: center;
            max-width: 90%;
        }
        .event-notification.show {
            display: block;
        }

        .wheel-overlay {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(4px);
            z-index: 35;
            border-radius: 36px;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            padding: 30px;
        }
        .wheel-overlay.open {
            display: flex;
        }
        .wheel-box {
            background: #ffffff;
            border-radius: 32px;
            padding: 30px 24px;
            max-width: 400px;
            width: 100%;
            text-align: center;
            animation: popIn 0.4s ease;
        }
        .wheel-box .wheel-title {
            font-size: 1.4rem;
            font-weight: 700;
            color: #3d2c24;
        }
        .wheel-box .wheel-spin {
            font-size: 3rem;
            margin: 16px 0;
            animation: spin 2s ease-in-out;
        }
        @keyframes spin {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(720deg);
            }
        }
        .wheel-box .wheel-result {
            font-size: 1.1rem;
            font-weight: 600;
            color: #3d2c24;
            margin: 8px 0;
        }
        .wheel-box .wheel-desc {
            font-size: 0.85rem;
            color: #9a7a6a;
            margin-bottom: 16px;
        }
        .wheel-box button {
            padding: 10px 32px;
            border: 1px solid #d5c4b6;
            border-radius: 40px;
            background: #e8ddd2;
            font-weight: 600;
            color: #3d2c24;
            cursor: pointer;
            font-size: 0.9rem;
            transition: 0.15s;
        }
        .wheel-box button:active {
            transform: scale(0.95);
        }

        .ending-overlay {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(8px);
            z-index: 50;
            border-radius: 36px;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            padding: 30px;
        }
        .ending-overlay.open {
            display: flex;
        }
        .ending-box {
            background: #ffffff;
            border-radius: 40px;
            padding: 30px 24px;
            max-width: 400px;
            width: 100%;
            text-align: center;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            animation: popIn 0.5s ease;
        }
        .ending-box .ending-icon {
            font-size: 3.5rem;
            margin-bottom: 10px;
        }
        .ending-box .ending-title {
            font-size: 1.6rem;
            font-weight: 800;
            color: #3d2c24;
            margin-bottom: 6px;
        }
        .ending-box .ending-sub {
            color: #9a7a6a;
            font-size: 0.9rem;
            margin-bottom: 16px;
            line-height: 1.6;
        }
        .ending-box .ending-actions {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
        }
        .ending-box .ending-actions button {
            padding: 10px 24px;
            border: 1px solid #d5c4b6;
            border-radius: 40px;
            background: #ffffff;
            font-weight: 600;
            color: #3d2c24;
            cursor: pointer;
            font-size: 0.85rem;
            transition: 0.15s;
            min-width: 100px;
        }
        .ending-box .ending-actions button:active {
            transform: scale(0.95);
        }
        .ending-box .ending-actions .btn-primary {
            background: #e8ddd2;
            border-color: #d5c4b6;
        }

        .footer {
            text-align: center;
            color: #cbb8a8;
            font-size: 0.6rem;
            padding: 4px 0 2px;
        }
        @media (max-width: 480px) {
            .app {
                height: 98vh;
                max-height: none;
                border-radius: 20px;
            }
            .page-slide {
                padding: 10px;
            }
            .interact-modal .modal-actions {
                grid-template-columns: 1fr 1fr;
            }
            .chat-window {
                border-radius: 20px;
                padding: 10px;
            }
            .chat-input-area input {
                font-size: 0.8rem;
                padding: 8px 12px;
            }
            .chat-input-area .send-btn {
                padding: 8px 14px;
                font-size: 0.8rem;
                min-width: 50px;
            }
            .ending-box {
                padding: 20px 16px;
            }
            .ending-box .ending-title {
                font-size: 1.3rem;
            }
            .my-stats {
                grid-template-columns: 1fr 1fr;
            }
            .story-box {
                padding: 20px 16px;
                max-height: 70vh;
            }
        }
    </style>
</head>
<body>

<div class="app" id="appContainer">
    <div class="turn-display" id="turnDisplay">📅 第 0 / 30 回合</div>

    <div class="achievement-toast" id="achievementToast">🏆 解鎖成就！</div>
    <div class="event-notification" id="eventNotification">🌊 地獄島發生了事件！</div>

    <div class="swipe-container" id="swipeContainer">
        <!-- 頁面一：地獄島 -->
        <div class="page-slide" id="page1">
            <div class="header">
                <h1>🔥 單身即地獄 <small>終極版</small></h1>
                <div class="sub">✦ 點擊角色 · 主動互動 ✦</div>
            </div>

            <div class="stamina-bar">
                <span class="label">⚡ 體力</span>
                <div class="track"><div class="fill" id="staminaFill" style="width:100%"></div></div>
                <span class="value" id="staminaText">100/100</span>
            </div>

            <div class="status-bar">
                <span class="status-item">🏝️ 地獄島</span>
                <span class="status-item">✦ 單身 <span class="num" id="remainingCount">6</span></span>
                <span class="status-item">💞 配對 <span class="num" id="pairCount">0</span></span>
                <span class="status-item">💰 <span class="num" id="moneyDisplay">1500</span></span>
            </div>

            <div class="player-section">
                <div style="font-weight:600; color:#9a7a6a; font-size:0.75rem;">🎯 選擇你的角色</div>
                <div class="player-select" id="playerSelect"></div>
                <button class="btn-sm" id="clearPlayerBtn" style="width:100%; margin-top:4px;">🚫 取消扮演</button>
            </div>

            <div class="roster">
                <div class="gender-group">
                    <div class="gender-label">👨 男性 <span style="font-size:0.6rem;color:#9a7a6a;">點擊頭像互動</span></div>
                    <div class="avatar-list" id="menContainer"></div>
                </div>
                <div class="gender-group">
                    <div class="gender-label">👩 女性 <span style="font-size:0.6rem;color:#9a7a6a;">點擊頭像互動</span></div>
                    <div class="avatar-list" id="womenContainer"></div>
                </div>
            </div>

            <div class="rest-area">
                <button class="rest-btn" id="restBtn">💤 休息（過一回合）</button>
            </div>

            <div class="log-area" id="logArea">
                <div class="log-line">🌸 選擇角色後，點擊任何單身異性展開互動！</div>
            </div>
            <div class="log-toolbar">
                <button class="btn-sm" id="clearLogBtn">🗑️ 清空日誌</button>
                <button class="btn-sm" id="resetBtn">🔄 重啟</button>
            </div>
            <div class="footer">👆 左右滑動 → 手機通訊</div>
        </div>

        <!-- 頁面二：手機通訊 -->
        <div class="page-slide" id="page2">
            <div class="phone-header">
                <h2>📱 節目組手機</h2>
                <span class="status-dot"></span>
                <span style="font-size:0.65rem; color:#9a7a6a;">連線中</span>
            </div>
            <div style="display:flex; gap:4px; background:#f5efe8; border-radius:50px; padding:4px; margin-bottom:10px; border:1px solid #ede4db;">
                <button class="tab-btn-phone active" data-tab="kakao">💬 KakaoTalk</button>
                <button class="tab-btn-phone" data-tab="instagram">📸 Instagram</button>
                <button class="tab-btn-phone" data-tab="ranking">🏆 排行榜</button>
                <button class="tab-btn-phone" data-tab="diary">📖 日記</button>
            </div>
            <div id="kakaoTab"><div class="chat-list" id="chatList"></div></div>
            <div id="instagramTab" style="display:none;"><div id="igContent"></div></div>
            <div id="rankingTab" style="display:none;">
                <div style="font-weight:600; color:#3d2c24; font-size:0.9rem; padding:8px 0 4px;">❤️ 好感度排行榜</div>
                <div id="rankingContent"></div>
            </div>
            <div id="diaryTab" style="display:none;">
                <div style="font-weight:600; color:#3d2c24; font-size:0.9rem; padding:8px 0 4px;">📖 回憶日記</div>
                <div id="diaryContent" style="font-size:0.8rem; color:#6b5a4e; line-height:1.6;"></div>
            </div>
            <div class="chat-window" id="chatWindow">
                <div class="chat-header">
                    <button class="back" id="chatBackBtn">‹</button>
                    <span class="name" id="chatPartnerName">嘉賓</span>
                    <span class="status-text" id="chatPartnerStatus">線上</span>
                </div>
                <div class="chat-messages" id="chatMessages"><div class="msg received">안녕하세요~ 你好！</div></div>
                <div class="chat-input-area">
                    <input type="text" id="chatInput" placeholder="輸入訊息..." maxlength="100" autofocus>
                    <button class="send-btn" id="chatSendBtn">發送</button>
                </div>
            </div>
        </div>

        <!-- 頁面三：我的 -->
        <div class="page-slide" id="page3">
            <div class="header">
                <h1>👤 我的 <small>狀態</small></h1>
                <div class="sub">✦ 體力 · 金錢 · 配對 · 成就 ✦</div>
            </div>

            <div class="my-profile" id="myProfile">
                <div class="my-avatar-wrapper">
                    <div class="my-avatar" id="myAvatar" onclick="changeAvatar()">👤</div>
                    <span class="edit-hint">✎ 點擊頭像更換照片</span>
                </div>
                <div class="my-name" id="myName">未選擇角色</div>
                <div class="my-status" id="myStatus">💔 單身</div>
            </div>

            <div class="my-stats">
                <div class="my-stat-card"><div class="stat-icon">⚡</div><div class="stat-value" id="myStamina">100</div><div class="stat-label">體力</div></div>
                <div class="my-stat-card"><div class="stat-icon">💰</div><div class="stat-value" id="myMoney">1500</div><div class="stat-label">金錢</div></div>
                <div class="my-stat-card"><div class="stat-icon">🏆</div><div class="stat-value" id="myAchievementCount">0</div><div class="stat-label">成就</div></div>
                <div class="my-stat-card"><div class="stat-icon">📖</div><div class="stat-value" id="myStoryCount">0</div><div class="stat-label">故事解鎖</div></div>
            </div>

            <div class="my-partner">
                <div class="partner-label">💞 配對對象</div>
                <div class="partner-name" id="myPartner">尚未配對</div>
            </div>

            <div class="my-actions">
                <button class="btn-primary" id="myRestBtn">💤 休息（恢復體力）</button>
                <button id="mySaveBtn">💾 存檔</button>
            </div>

            <input type="file" id="avatarInput" accept="image/*" style="display:none" onchange="handleAvatarUpload(event)">

            <!-- 成就列表 -->
            <div class="achievement-list">
                <div class="ach-title">🏆 已解鎖成就</div>
                <div id="myAchievementList" style="font-size:0.75rem; color:#6b5a4e; padding:2px 0; min-height:20px;">
                    尚未解鎖任何成就
                </div>
            </div>

            <div style="margin-top:10px; background:#faf6f2; border-radius:20px; padding:10px 14px; border:1px solid #ede4db;">
                <div style="font-size:0.7rem; color:#9a7a6a; font-weight:600;">📋 遊戲提示</div>
                <div style="font-size:0.7rem; color:#6b5a4e; margin-top:4px; line-height:1.5;">
                    • 每個動作消耗 20 體力<br>
                    • 體力歸零時強制休息（過一回合）<br>
                    • 送禮物會花錢，但能增加好感度<br>
                    • 解鎖角色故事可獲得額外好感度獎勵<br>
                    • 收集成就可以獲得特殊稱號
                </div>
            </div>

            <div class="footer">👆 左右滑動切換頁面</div>
        </div>
    </div>

    <div class="swipe-nav" id="swipeNav">
        <button class="active" data-page="0">🏝️ 地獄島</button>
        <button data-page="1">📱 手機</button>
        <button data-page="2">👤 我的</button>
    </div>

    <div class="interact-modal" id="interactModal">
        <div class="modal-title" id="modalTitle">💬 與 志赫 互動</div>
        <div class="modal-sub" id="modalSub">❤️ 好感度：0 | 關係：單身</div>
        <div class="modal-actions" id="modalActions">
            <button class="btn-primary" data-action="chat">💬 私下聊天</button>
            <button class="btn-heart" data-action="confess">💌 告白</button>
            <button class="btn-light" data-action="observe">👀 觀察對方</button>
            <button class="btn-primary" data-action="gift">🎁 送禮物</button>
            <button class="btn-info" data-action="gossip">📢 打聽消息</button>
        </div>
        <button class="modal-close" id="modalClose">✕ 取消</button>
    </div>

    <div class="story-overlay" id="storyOverlay">
        <div class="story-box">
            <div class="story-header">
                <span class="story-avatar" id="storyAvatar">🦁</span>
                <span class="story-name" id="storyName">志赫</span>
                <span class="story-chapter" id="storyChapter">第一章</span>
            </div>
            <div class="story-dialogue" id="storyDialogue">對話內容</div>
            <div class="story-choices" id="storyChoices"></div>
            <div class="story-result" id="storyResult"></div>
            <button class="story-skip" id="storySkipBtn">⏭️ 跳過故事（不會獲得獎勵）</button>
        </div>
    </div>

    <div class="wheel-overlay" id="wheelOverlay">
        <div class="wheel-box">
            <div class="wheel-title">🎡 命運轉盤</div>
            <div class="wheel-spin" id="wheelSpin">🎰</div>
            <div class="wheel-result" id="wheelResult">結果</div>
            <div class="wheel-desc" id="wheelDesc">描述</div>
            <button id="wheelConfirmBtn">確認</button>
        </div>
    </div>

    <div class="ending-overlay" id="endingOverlay">
        <div class="ending-box">
            <div class="ending-icon" id="endingIcon">💕</div>
            <div class="ending-title" id="endingTitle">結局</div>
            <div class="ending-sub" id="endingSub">描述</div>
            <div class="ending-actions">
                <button class="btn-primary" id="endingSaveBtn">💾 存檔</button>
                <button id="endingRestartBtn">🔄 重新開始</button>
            </div>
        </div>
    </div>

    <audio id="heAudio" preload="auto"><source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg"></audio>
    <audio id="beAudio" preload="auto"><source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3" type="audio/mpeg"></audio>
</div>

<script>
(function() {
    // ============================================================
    // 角色設定
    // ============================================================
    const MEN = [
        { id: 'm1', name: '志赫', emoji: '🦁', personality: '熱情型', personalityDesc: '主動、愛開玩笑，善於帶動氣氛' },
        { id: 'm2', name: '俊浩', emoji: '🐺', personality: '溫暖型', personalityDesc: '話少但真摯，給人安全感' },
        { id: 'm3', name: '載勳', emoji: '🔥', personality: '熱情型', personalityDesc: '直球告白型，不拐彎抹角' },
        { id: 'm4', name: '泰源', emoji: '🐉', personality: '溫暖型', personalityDesc: '細心、會關心人，暖男類型' },
        { id: 'm5', name: '民碩', emoji: '🦅', personality: '幽默型', personalityDesc: '擅長製造氛圍，聊天高手' },
        { id: 'm6', name: '正宇', emoji: '⚡', personality: '高冷型', personalityDesc: '話不多但有毒舌魅力' }
    ];

    const WOMEN = [
        { id: 'w1', name: '智雅', emoji: '🌸', personality: '高冷型', personalityDesc: '懂得推拉、不卑不亢' },
        { id: 'w2', name: '秀珍', emoji: '🌺', personality: '熱情型', personalityDesc: '主動找話題、愛笑，陽光型' },
        { id: 'w3', name: '藝琳', emoji: '🌹', personality: '溫暖型', personalityDesc: '善解人意、回應溫暖' },
        { id: 'w4', name: '娜英', emoji: '🌷', personality: '直率型', personalityDesc: '有話直說、不拐彎' },
        { id: 'w5', name: '惠善', emoji: '🌻', personality: '文靜型', personalityDesc: '害羞但真誠，需要耐心' },
        { id: 'w6', name: '敏靜', emoji: '🌿', personality: '幽默型', personalityDesc: '擅長試探、話中有話' }
    ];

    const ALL_CHARS = [...MEN, ...WOMEN];

    // ============================================================
    // 角色專屬故事（12 位 × 3 章節）
    // ============================================================
    const STORIES = {
        'm1': [{ chapter: 1, title: '🔥 火種', triggerAffection: 30, dialogue: '【夜晚營火旁】\n\n志赫撥弄著火堆，沉默了一會兒。\n\n「你知道嗎？我以前不是這樣的。」\n\n「小時候我被霸凌過，因為我長得瘦小。後來我開始健身、改變自己。我學會了，與其等別人認同你，不如讓自己強大到不需要認同。」\n\n他抬起頭，眼神真摯。\n\n「但對你，我不想假裝強大。我想讓你知道真實的我。」', choices: [{ text: '💪 你很勇敢，我很佩服你', result: '志赫笑了，眼中閃過一絲感動。\n\n「謝謝你...這是我第一次跟別人說這些。」\n\n❤️ 好感度 +8', affDelta: 8 }, { text: '🤗 你可以在我面前軟弱，沒關係', result: '志赫愣了一下，然後低下頭。\n\n「從來沒有人對我說過這句話...」\n\n他的聲音有些哽咽。\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 過去的都過去了，你現在很好', result: '志赫露出溫柔的笑容。\n\n「是啊...因為有你，我現在覺得很好。」\n\n❤️ 好感度 +6', affDelta: 6 }] },
            { chapter: 2, title: '💭 真心話', triggerAffection: 60, dialogue: '【海邊散步】\n\n志赫突然停下腳步，轉身面對你。\n\n「你知道我為什麼總是笑嗎？」\n\n「因為我不想讓別人看到我認真起來的樣子。我害怕認真了卻失敗，那比不認真還痛苦。」\n\n他深吸一口氣。\n\n「但對你，我不想隱藏了。我想認真地對待你。」', choices: [{ text: '❤️ 我也想認真對待你', result: '志赫的眼中閃過光芒。\n\n「真的嗎？太好了...」\n\n他輕輕握住你的手。\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 慢慢來吧，我還在認識你', result: '志赫點了點頭。\n\n「好，我等你。我會一直等你。」\n\n❤️ 好感度 +5', affDelta: 5 }, { text: '💕 我喜歡你認真的樣子', result: '志赫笑了，是那種真正的笑。\n\n「那我以後只對你認真。」\n\n❤️ 好感度 +12', affDelta: 12 }] },
            { chapter: 3, title: '🌌 承諾', triggerAffection: 85, dialogue: '【星空下】\n\n志赫仰望著星空，聲音很輕。\n\n「我害怕自己不夠好，配不上你。我總是裝作很自信，但其實我還是那個會被別人說『你不夠好』的小男孩。」\n\n他轉向你，眼神堅定。\n\n「但我想試試看。用一輩子證明我值得你喜歡。」', choices: [{ text: '💕 你已經夠好了，我喜歡現在的你', result: '志赫的眼中泛起淚光。\n\n「謝謝你...這是我這輩子聽過最好的話。」\n\n他緊緊抱住你。\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我們一起變好，好嗎？', result: '志赫點頭，臉上帶著溫暖的笑。\n\n「好。一起。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我願意相信你', result: '志赫握住你的手。\n\n「我不會讓你失望的。我保證。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'm2': [{ chapter: 1, title: '💔 傷痕', triggerAffection: 30, dialogue: '【雨天屋簷下】\n\n俊浩安靜地看著雨滴落下。\n\n「我曾經有一段三年的感情。因為我不擅長表達，她離開了。」\n\n他轉向你，眼神平靜。\n\n「我不會說漂亮話，但我會用行動證明。如果你願意給我機會。」', choices: [{ text: '🤝 我願意給你機會', result: '俊浩眼中閃過一絲光芒。\n\n「謝謝你...我會用行動證明。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 行動比言語更重要', result: '俊浩微微點頭。\n\n「你懂我。謝謝。」\n\n❤️ 好感度 +8', affDelta: 8 }, { text: '💔 聽起來你很受傷', result: '俊浩沉默了一會兒。\n\n「...你是第一個這樣說的人。」\n\n❤️ 好感度 +6', affDelta: 6 }] },
            { chapter: 2, title: '🛡️ 守護', triggerAffection: 60, dialogue: '【廚房做飯時】\n\n俊浩正在切菜，頭也不回地說。\n\n「我記性不好，但關於你的事，我都記得。你喜歡吃什麼、不喜歡什麼、什麼時候會笑...」\n\n他停下手，轉向你。\n\n「因為你對我來說很重要。」', choices: [{ text: '💕 你讓我覺得被在乎', result: '俊浩微微臉紅。\n\n「...因為你值得。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 我也記得你的事', result: '俊浩愣了一下，然後笑了。\n\n「真的嗎？...我很開心。」\n\n❤️ 好感度 +8', affDelta: 8 }, { text: '❤️ 有你真好', result: '俊浩低著頭，聲音有些哽咽。\n\n「...我也是。有你在，真好。」\n\n❤️ 好感度 +12', affDelta: 12 }] },
            { chapter: 3, title: '🏠 歸宿', triggerAffection: 85, dialogue: '【夕陽下的沙灘】\n\n俊浩望著夕陽，聲音平靜而堅定。\n\n「我不知道未來會怎樣，但我知道我想跟你一起走。」\n\n他轉向你。\n\n「你不用急著回答。我只是想讓你知道，你是我第一個想共度餘生的人。」', choices: [{ text: '💕 我也想跟你一起走', result: '俊浩的眼中泛起淚光。\n\n「...這是我這輩子聽過最好的話。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我會好好考慮的', result: '俊浩微笑著點頭。\n\n「好。我等你。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你的心意我收到了', result: '俊浩輕輕握住你的手。\n\n「那就夠了。」\n\n❤️ 好感度 +8', affDelta: 8 }] }],
        'm3': [{ chapter: 1, title: '💌 告白', triggerAffection: 30, dialogue: '【人群之中】\n\n載勳突然站起來，大聲說。\n\n「我喜歡你！不是開玩笑的！」\n\n全場安靜下來。他看著你，眼神認真。\n\n「這是我第一次這麼認真。因為是你。」', choices: [{ text: '💕 我也喜歡你', result: '載勳露出燦爛的笑容。\n\n「太好了！我就知道！」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 我需要時間想想', result: '載勳點頭。\n\n「好，我等你。但我會一直喜歡你。」\n\n❤️ 好感度 +5', affDelta: 5 }, { text: '❤️ 你好勇敢', result: '載勳笑了。\n\n「因為是你，我才勇敢。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 2, title: '😢 脆弱', triggerAffection: 60, dialogue: '【無人的海邊】\n\n載勳坐在沙灘上，聲音低沉。\n\n「其實我每次都先告白，是因為我害怕。與其等別人來傷我，不如我先攤牌。」\n\n他抬起頭，苦笑著。\n\n「但對你，我不是因為害怕。我是因為確定。」', choices: [{ text: '💕 確定了什麼？', result: '載勳認真地看著你。\n\n「確定了你就是我要的那個人。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '🤗 你不用總是這麼堅強', result: '載勳眼眶泛紅。\n\n「謝謝你...這句話比什麼都好。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我相信你', result: '載勳笑了。\n\n「那就夠了。」\n\n❤️ 好感度 +6', affDelta: 6 }] },
            { chapter: 3, title: '🔥 不退', triggerAffection: 85, dialogue: '【日出時分】\n\n載勳站在海邊，迎著晨光。\n\n「以前我告白是因為怕輸。但這次不一樣。」\n\n他轉向你，眼中倒映著日出。\n\n「這次是因為我確定，你就是我要的那個人。不管結果如何，我都會喜歡你。」', choices: [{ text: '💕 我也確定是你', result: '載勳緊緊抱住你。\n\n「這是我人生中最幸福的一刻。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我會一直陪著你', result: '載勳微笑著。\n\n「那就夠了。有你在身邊，我什麼都不怕。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 你的心意我收到了', result: '載勳點頭。\n\n「我會繼續努力，讓你看到我的心意。」\n\n❤️ 好感度 +8', affDelta: 8 }] }],
        'm4': [{ chapter: 1, title: '🍲 照顧', triggerAffection: 30, dialogue: '【你生病時】\n\n泰源默默煮了一碗粥給你。\n\n「我以前也照顧過我妹妹，所以你不用感到不好意思。」\n\n他坐在你旁邊，眼神溫暖。\n\n「好好休息，我會照顧你。」', choices: [{ text: '😊 謝謝你，你好溫柔', result: '泰源微微笑了。\n\n「能照顧你，我很開心。」\n\n❤️ 好感度 +8', affDelta: 8 }, { text: '💕 你讓我有安全感', result: '泰源的眼神變得柔和。\n\n「能讓你有安全感，是我的榮幸。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '❤️ 我也想照顧你', result: '泰源愣了一下，然後笑了。\n\n「好。那我們互相照顧。」\n\n❤️ 好感度 +12', affDelta: 12 }] },
            { chapter: 2, title: '🌙 秘密', triggerAffection: 60, dialogue: '【深夜聊天時】\n\n泰源望著星空，聲音低沉。\n\n「我其實很怕孤單，所以總是把別人照顧好，讓自己感覺被需要。」\n\n他轉向你，眼神帶著一絲脆弱。\n\n「你知道嗎？我也需要有人照顧我。」', choices: [{ text: '💕 我會照顧你', result: '泰源眼眶泛紅。\n\n「謝謝你...你是第一個這樣說的人。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '🤗 你可以依賴我', result: '泰源輕輕點頭。\n\n「我會試著學習依賴你。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你值得被照顧', result: '泰源露出了溫暖的笑容。\n\n「謝謝你...這句話對我來說很重要。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 3, title: '🤝 陪伴', triggerAffection: 85, dialogue: '【星空下】\n\n泰源握住你的手，聲音溫柔。\n\n「我想照顧你一輩子，但我也希望你能照顧我。」\n\n他微笑著。\n\n「我們互相依偎，好不好？」', choices: [{ text: '💕 好，我們互相依偎', result: '泰源的眼中泛起淚光。\n\n「這是我聽過最美的承諾。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我願意陪你', result: '泰源緊緊握住你的手。\n\n「那就夠了。有你在，我不再孤單。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我們一起走下去', result: '泰源微笑著。\n\n「好。一起。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'm5': [{ chapter: 1, title: '🎭 面具', triggerAffection: 30, dialogue: '【搞笑之後】\n\n民碩突然安靜下來。\n\n「我喜歡逗大家笑，但我自己其實不常笑。」\n\n他低下頭。\n\n「我用幽默蓋住自己的孤獨。但跟你在一起的時候，我不需要那樣。」', choices: [{ text: '💕 你可以做真實的自己', result: '民碩抬起頭，眼中閃著光。\n\n「你是第一個讓我覺得可以不用搞笑的人。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '🤗 我喜歡真實的你', result: '民碩笑了，是那種真心的笑。\n\n「謝謝你...我好開心。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 你不需要偽裝', result: '民碩點頭。\n\n「好。在你面前，我不偽裝了。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 2, title: '💖 真心', triggerAffection: 60, dialogue: '【獨處時】\n\n民碩認真地看著你。\n\n「你是我第一個覺得『不用搞笑也沒關係』的人。」\n\n他停頓了一下。\n\n「跟你在的時候，我可以做自己。」', choices: [{ text: '💕 我喜歡你做自己', result: '民碩露出了溫暖的笑容。\n\n「你讓我覺得，被接納的感覺真好。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '❤️ 你已經夠好了', result: '民碩眼眶微微泛紅。\n\n「謝謝你...這句話比任何笑話都讓我開心。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我喜歡真實的你', result: '民碩笑了。\n\n「那我要把最好的自己給你。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 3, title: '🌅 未來', triggerAffection: 85, dialogue: '【夕陽下】\n\n民碩望著遠方，聲音平靜。\n\n「以前我覺得未來很遙遠，但現在我開始想像我們一起變老的樣子。」\n\n他轉向你。\n\n「我想跟你有個未來。」', choices: [{ text: '💕 我也想跟你一起變老', result: '民碩的眼眶泛淚。\n\n「這是我聽過最美的話。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我們一起創造未來', result: '民碩微笑著。\n\n「好。一起創造屬於我們的未來。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我願意跟你走', result: '民碩握住你的手。\n\n「那就夠了。我們走吧。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'm6': [{ chapter: 1, title: '📏 距離', triggerAffection: 30, dialogue: '【保持距離時】\n\n正宇看著遠方。\n\n「我習慣跟人保持距離，不是因為討厭，而是因為太靠近就會受傷。」\n\n他轉向你。\n\n「但你讓我覺得，也許靠近一點也不錯。」', choices: [{ text: '💕 我會慢慢靠近你', result: '正宇沉默了一會兒。\n\n「...好。我會試著不逃開。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '🤗 你可以相信我', result: '正宇的眼神柔和了一些。\n\n「...我第一次覺得，也許可以相信一個人。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 慢慢來就好', result: '正宇微微點頭。\n\n「嗯。謝謝你願意等我。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 2, title: '🔓 信任', triggerAffection: 60, dialogue: '【深夜談心時】\n\n正宇的聲音很低。\n\n「我曾經被最信任的人背叛，從此不再輕易相信人。」\n\n他抬起頭，看著你。\n\n「你是第一個讓我覺得『可以相信』的人。」', choices: [{ text: '💕 我會珍惜你的信任', result: '正宇的眼中閃過一絲波動。\n\n「...謝謝你。我會努力不讓你失望。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '❤️ 你可以相信我', result: '正宇沉默了很久。\n\n「...好。我相信你。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '🤗 我會一直站在你身邊', result: '正宇的眼眶微微泛紅。\n\n「...從來沒有人對我說過這句話。」\n\n❤️ 好感度 +15', affDelta: 15 }] },
            { chapter: 3, title: '💞 靠近', triggerAffection: 85, dialogue: '【安靜的海邊】\n\n正宇站在你身邊，聲音很輕。\n\n「我想跨過那條線，離你近一點。」\n\n他轉向你。\n\n「即使害怕，我也想試試看。」', choices: [{ text: '💕 我也希望靠近你', result: '正宇輕輕握住你的手。\n\n「...謝謝你。我不會後悔的。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 你已經很勇敢了', result: '正宇的眼中閃著光。\n\n「因為是你，我才勇敢。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我會陪你面對恐懼', result: '正宇微笑了。\n\n「好。有你在，我不怕了。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'w1': [{ chapter: 1, title: '💎 完美', triggerAffection: 30, dialogue: '【眾人面前】\n\n智雅微笑著，但眼神有一絲疲憊。\n\n「大家都覺得我完美，但我知道我不是。」\n\n她低下頭。\n\n「我只是不讓別人看到我的不完美。」', choices: [{ text: '💕 我喜歡真實的你', result: '智雅抬起頭，眼中閃著光。\n\n「從來沒有人這樣對我說過...」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '🤗 你不用總是完美', result: '智雅的眼神柔和了。\n\n「在你面前，我想試著放下。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 你已經夠好了', result: '智雅露出了真心的笑容。\n\n「謝謝你...這句話對我來說很珍貴。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 2, title: '💄 卸妝', triggerAffection: 60, dialogue: '【獨處時】\n\n智雅放下了一貫的優雅。\n\n「你讓我覺得，我可以不用那麼累。」\n\n她笑了。\n\n「可以不用一直維持完美的樣子。」', choices: [{ text: '💕 我喜歡你真實的樣子', result: '智雅的眼眶泛淚。\n\n「謝謝你...你讓我覺得被接納了。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '❤️ 你可以放鬆做自己', result: '智雅輕聲說。\n\n「在你面前，我願意放鬆。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你已經很好了', result: '智雅笑了。\n\n「能遇到你，是我最大的幸運。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 3, title: '🌸 真實', triggerAffection: 85, dialogue: '【日出時】\n\n智雅轉身面對你。\n\n「我想把我最真實的樣子給你看，包括所有的不完美。」\n\n她的眼神堅定。\n\n「你願意接受這樣的我嗎？」', choices: [{ text: '💕 我願意接受全部的你', result: '智雅緊緊抱住你。\n\n「謝謝你...我好幸福。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 你的不完美我也喜歡', result: '智雅的眼中閃著淚光。\n\n「這是我聽過最動人的話。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我喜歡的是你這個人', result: '智雅微笑著。\n\n「那就夠了。我願意把所有都給你。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'w2': [{ chapter: 1, title: '😊 笑容', triggerAffection: 30, dialogue: '【開心過後】\n\n秀珍的笑容收斂了一下。\n\n「很多人都喜歡我的笑容，但不知道我也會難過。」\n\n她低下頭。\n\n「我只是不想把壞情緒帶給別人。」', choices: [{ text: '💕 你可以難過，沒關係', result: '秀珍抬起頭，眼中閃著淚光。\n\n「謝謝你...你讓我覺得可以放心難過。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '🤗 我會聽你說', result: '秀珍露出了溫暖的笑容。\n\n「有你願意聽，我就很開心了。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 你的開心很重要', result: '秀珍笑著點頭。\n\n「我會記得開心的。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 2, title: '🔋 疲憊', triggerAffection: 60, dialogue: '【安靜時刻】\n\n秀珍坐在你旁邊。\n\n「有時候我也很累，但看到你我就覺得有力量了。」\n\n她笑了。\n\n「你就是我的充電器。」', choices: [{ text: '💕 我也會陪你充電', result: '秀珍笑了。\n\n「有你這句話，我就可以再撐下去了。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '❤️ 你永遠可以依靠我', result: '秀珍的眼眶泛紅。\n\n「謝謝你...你是我最安心的依靠。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 看著你笑我也開心', result: '秀珍笑著說。\n\n「那我要多笑一點，因為你喜歡。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 3, title: '🤝 依靠', triggerAffection: 85, dialogue: '【夕陽下】\n\n秀珍認真地看著你。\n\n「我想在你面前不用堅強，可以當一個軟弱的人。」\n\n她輕聲問。\n\n「你願意當我的依靠嗎？」', choices: [{ text: '💕 我願意當你的依靠', result: '秀珍感動地抱住你。\n\n「有你在，我什麼都不怕了。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 你可以依賴我', result: '秀珍笑了。\n\n「好。那我要開始學習依賴你了。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我一直都在', result: '秀珍微笑著。\n\n「那就夠了。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'w3': [{ chapter: 1, title: '💝 付出', triggerAffection: 30, dialogue: '【為你準備東西時】\n\n藝琳微笑著。\n\n「我習慣對人好，因為我害怕別人離開。」\n\n她抬起頭。\n\n「但對你，我是真的想對你好。」', choices: [{ text: '💕 你已經做得很好了', result: '藝琳眼眶泛淚。\n\n「謝謝你...有你這句話就夠了。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '❤️ 我不會離開', result: '藝琳笑了。\n\n「有你這句話，我就安心了。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 你的用心我都知道', result: '藝琳的眼中閃著光。\n\n「被看見的感覺，真的很好。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 2, title: '💪 勇敢', triggerAffection: 60, dialogue: '【緊張的告白】\n\n藝琳鼓起勇氣。\n\n「我一直不敢說出口，但我喜歡你。」\n\n她低下頭。\n\n「不是因為你對我好，而是因為你是你。」', choices: [{ text: '💕 我也喜歡你', result: '藝琳驚喜地抬頭。\n\n「真的嗎？我好開心...」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '❤️ 你很勇敢', result: '藝琳笑了。\n\n「因為是你，我才勇敢。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你的心意我收到了', result: '藝琳微笑著。\n\n「那就夠了。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 3, title: '🤗 擁抱', triggerAffection: 85, dialogue: '【溫暖的夜晚】\n\n藝琳輕聲說。\n\n「我想擁抱你，不只是現在，而是每一個明天。」\n\n她問。\n\n「你會一直在我身邊嗎？」', choices: [{ text: '💕 我會一直在你身邊', result: '藝琳感動地落淚。\n\n「這是我這輩子聽過最好的承諾。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我永遠都在', result: '藝琳笑了。\n\n「有你在，我就滿足了。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我會陪你走完每一天', result: '藝琳微笑著。\n\n「好。每一天。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'w4': [{ chapter: 1, title: '🎯 直球', triggerAffection: 30, dialogue: '【直接告白】\n\n娜英看著你。\n\n「我喜歡你，我不喜歡拐彎抹角。」\n\n她笑了。\n\n「我喜歡就是喜歡，沒有理由。」', choices: [{ text: '💕 我也喜歡你', result: '娜英開心地笑了。\n\n「我就知道！我眼光很好！」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你好直接啊', result: '娜英笑著說。\n\n「對你就是要直接。」\n\n❤️ 好感度 +8', affDelta: 8 }, { text: '❤️ 我喜歡你的勇氣', result: '娜英的眼神變得更認真。\n\n「因為是你，我才敢這麼勇敢。」\n\n❤️ 好感度 +12', affDelta: 12 }] },
            { chapter: 2, title: '😢 不安', triggerAffection: 60, dialogue: '【脆弱時刻】\n\n娜英的聲音低了一些。\n\n「我裝得很堅強，但我其實很怕被拒絕。」\n\n她看著你。\n\n「因為我從來沒有這麼喜歡過一個人。」', choices: [{ text: '💕 我不會拒絕你', result: '娜英的眼眶泛紅。\n\n「你是第一個讓我覺得安全的人。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '❤️ 你的喜歡我會珍惜', result: '娜英笑了。\n\n「謝謝你...你讓我有勇氣繼續喜歡你。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你不用堅強，有我在', result: '娜英的眼淚滑落。\n\n「...從來沒有人對我說過這句話。」\n\n❤️ 好感度 +15', affDelta: 15 }] },
            { chapter: 3, title: '💍 承諾', triggerAffection: 85, dialogue: '【堅定的眼神】\n\n娜英認真地看著你。\n\n「我會用一輩子證明，你選擇我是對的。」\n\n她笑了。\n\n「我不會說好聽話，但我的行動會說話。」', choices: [{ text: '💕 我相信你', result: '娜英笑了，帶著淚光。\n\n「謝謝你相信我。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我會看著你的行動', result: '娜英微笑著。\n\n「好。我不會讓你失望。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我願意賭一把', result: '娜英開心地笑了。\n\n「我不會讓你輸的。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'w5': [{ chapter: 1, title: '🎤 聲音', triggerAffection: 30, dialogue: '【鼓起勇氣說話】\n\n惠善低著頭。\n\n「我很少說話，但跟你在一起的時候，我想說很多話。」\n\n她抬起頭，微笑著。\n\n「因為你會聽。」', choices: [{ text: '💕 我喜歡聽你說話', result: '惠善的眼中閃著光芒。\n\n「謝謝你...我好開心。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你說的話我都會認真聽', result: '惠善笑了。\n\n「那我要多說一點。」\n\n❤️ 好感度 +8', affDelta: 8 }, { text: '❤️ 你的聲音很好聽', result: '惠善的臉紅了。\n\n「第一次有人這樣說...」\n\n❤️ 好感度 +12', affDelta: 12 }] },
            { chapter: 2, title: '⏳ 等待', triggerAffection: 60, dialogue: '【默默陪伴時】\n\n惠善坐在你旁邊。\n\n「我一直在等你發現我。」\n\n她微笑。\n\n「不是因為我沒勇氣，而是因為我想等你主動。」', choices: [{ text: '💕 我發現你了', result: '惠善的眼眶濕了。\n\n「你終於發現我了...」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '❤️ 謝謝你等我', result: '惠善笑了。\n\n「等你多久我都願意。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 以後我會主動找你', result: '惠善的眼中閃著光。\n\n「我會等你的。」\n\n❤️ 好感度 +8', affDelta: 8 }] },
            { chapter: 3, title: '🌻 綻放', triggerAffection: 85, dialogue: '【自信的時刻】\n\n惠善抬起頭，眼神堅定。\n\n「我想為你勇敢一次。」\n\n她微笑。\n\n「我想讓你知道，我也可以是你依靠的人。」', choices: [{ text: '💕 我也想成為你的依靠', result: '惠善的眼中泛淚。\n\n「好。我們互相依靠。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 你已經很勇敢了', result: '惠善笑了。\n\n「因為有你，我才敢勇敢。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我會讓你依靠', result: '惠善微笑著。\n\n「那就夠了。」\n\n❤️ 好感度 +10', affDelta: 10 }] }],
        'w6': [{ chapter: 1, title: '🧠 試探', triggerAffection: 30, dialogue: '【聰明對話時】\n\n敏靜微笑著。\n\n「我習慣試探別人，因為我想知道對方是不是真心。」\n\n她看著你。\n\n「對你，我試探過，結果是我淪陷了。」', choices: [{ text: '💕 我也對你淪陷了', result: '敏靜笑了，帶著驚喜。\n\n「真的嗎？我以為只有我一個人這樣。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '😊 你不需要試探我', result: '敏靜的眼神柔和了。\n\n「好。以後不試探你了。」\n\n❤️ 好感度 +8', affDelta: 8 }, { text: '❤️ 我對你是真心的', result: '敏靜認真地看著你。\n\n「我相信你。」\n\n❤️ 好感度 +12', affDelta: 12 }] },
            { chapter: 2, title: '🛡️ 坦誠', triggerAffection: 60, dialogue: '【放下防備時】\n\n敏靜的聲音低了一些。\n\n「我總是保護自己，因為太聰明的人容易受傷。」\n\n她看著你。\n\n「但對你，我不想設防了。」', choices: [{ text: '💕 我會珍惜你的信任', result: '敏靜微笑著。\n\n「你是第一個讓我願意放下防備的人。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '❤️ 你可以相信我', result: '敏靜的眼神變得更柔和。\n\n「好。我相信你。」\n\n❤️ 好感度 +10', affDelta: 10 }, { text: '🤗 我會保護你', result: '敏靜的眼眶泛紅。\n\n「從來沒有人說過要保護我...」\n\n❤️ 好感度 +15', affDelta: 15 }] },
            { chapter: 3, title: '💎 選擇', triggerAffection: 85, dialogue: '【堅定的眼神】\n\n敏靜認真地看著你。\n\n「聰明的人知道什麼時候該放手，但我知道這次我不能放手。」\n\n她微笑。\n\n「因為你就是那個對的人。」', choices: [{ text: '💕 你也是我對的人', result: '敏靜感動地笑了。\n\n「太好了...我終於等到你了。」\n\n❤️ 好感度 +15', affDelta: 15 }, { text: '❤️ 我不會讓你失望', result: '敏靜微笑著。\n\n「我相信你。」\n\n❤️ 好感度 +12', affDelta: 12 }, { text: '😊 我們一起走下去', result: '敏靜點頭。\n\n「好。一起。」\n\n❤️ 好感度 +10', affDelta: 10 }] }]
    };

    // ============================================================
    // 成就系統
    // ============================================================
    const ACHIEVEMENTS = {
        'first_story': { name: '📖 故事啟程', desc: '解鎖第一個角色故事', icon: '📖' },
        'story_collector': { name: '📚 說書人', desc: '解鎖 5 個角色故事', icon: '📚' },
        'story_master': { name: '🏆 故事大師', desc: '解鎖 10 個角色故事', icon: '🏆' },
        'first_love': { name: '💕 初戀', desc: '第一次告白成功', icon: '💕' },
        'heart_breaker': { name: '💔 心碎獵人', desc: '被拒絕 3 次', icon: '💔' },
        'popular': { name: '🌟 人氣王', desc: '獲得人氣投票第一名', icon: '🌟' },
        'rich': { name: '💰 富翁', desc: '累積金錢超過 3000', icon: '💰' },
        'helper': { name: '🤝 暖心', desc: '送出 10 次禮物', icon: '🤝' },
        'survivor': { name: '🔥 生存者', desc: '完成 30 回合', icon: '🔥' },
        'perfect': { name: '💎 完美結局', desc: '達成 HE 結局', icon: '💎' }
    };

    // ============================================================
    // IG 貼文資料
    // ============================================================
    const IG_POSTS_DATA = {
        'm1': [{ content: '🔥 今天生火成功！雖然手很酸但超有成就感 💪 #地獄島生存', time: '2小時前' }, { content: '🌊 海邊的夕陽很美，但身邊少了一個人... #單身即地獄', time: '昨天' }, { content: '💪 健身時間！在地獄島也要保持身材 💪', time: '3天前' }],
        'm2': [{ content: '🌅 早安地獄島！新的一天新的挑戰 💪', time: '1小時前' }, { content: '📖 一個人靜靜看書的時光，很愜意 ☕', time: '2天前' }, { content: '🏋️ 今天跟志赫一起健身，他真的很認真', time: '4天前' }],
        'm3': [{ content: '🔥 熱情永遠是對的！今天也要全力以赴 💪', time: '3小時前' }, { content: '💕 有點在意某個人... 但不敢太主動 😅', time: '昨天' }, { content: '🏃 晨跑時看到日出，真的很美 🌅', time: '3天前' }],
        'm4': [{ content: '🌊 海風很舒服，心情也變好了 ☀️', time: '5小時前' }, { content: '🍳 今天做了早餐給大家吃，大家都說好吃 😊', time: '昨天' }, { content: '💭 想家了... 但這裡的風景也很棒', time: '5天前' }],
        'm5': [{ content: '😂 今天被載勳的冷笑話冷到不行，但還是很好笑', time: '2小時前' }, { content: '🎯 不管在哪裡，都要保持幽默感！😄', time: '昨天' }, { content: '💪 地獄島的生活雖然辛苦，但很有趣！', time: '3天前' }],
        'm6': [{ content: '⚡ 保持神秘，保持距離。', time: '1小時前' }, { content: '🌙 夜晚的星空很美，適合思考。', time: '昨天' }, { content: '🔥 不隨波逐流，做自己。', time: '6天前' }],
        'w1': [{ content: '🌸 今天穿了一件粉紅色的衣服，心情也變好了 💕', time: '2小時前' }, { content: '💋 保持優雅，保持從容。這是我的風格 ✨', time: '昨天' }, { content: '🌹 收到了匿名禮物... 會是誰呢？😊', time: '3天前' }],
        'w2': [{ content: '🌺 今天跟大家聊得很開心！地獄島其實沒那麼可怕 😊', time: '1小時前' }, { content: '💕 對某個人有點心動... 但還不確定對方的想法', time: '昨天' }, { content: '🎤 晚上大家唱歌的時候好歡樂！', time: '2天前' }],
        'w3': [{ content: '🌹 今天收到了一束花... 心跳好快 💕', time: '3小時前' }, { content: '🌸 溫柔對待每一個人，是我的人生哲學 😊', time: '昨天' }, { content: '📸 拍了一張很美的海景照，分享給大家 🌊', time: '4天前' }],
        'w4': [{ content: '🌷 有話直說是我的風格！喜歡就是喜歡 💪', time: '2小時前' }, { content: '💕 今天跟某人聊了很久，感覺很好 😊', time: '昨天' }, { content: '🔥 地獄島也要保持熱情！燃燒吧 🔥', time: '3天前' }],
        'w5': [{ content: '🌻 今天幫大家做飯了，看著大家吃得很開心我也開心 😊', time: '4小時前' }, { content: '💭 有點害羞... 但想跟某人多說幾句話', time: '昨天' }, { content: '📖 一個人看書的時候最放鬆了', time: '5天前' }],
        'w6': [{ content: '🌿 聰明是一種選擇，不是天賦 ✨', time: '1小時前' }, { content: '💕 今天試探了一下某個人，反應很有趣 😏', time: '昨天' }, { content: '🧠 觀察是最好的學習方式。', time: '4天前' }]
    };

    // ============================================================
    // 狀態（好感度全部從 0 開始）
    // ============================================================
    let state = {
        men: MEN.map(m => ({ ...m, paired: false, pairId: null })),
        women: WOMEN.map(w => ({ ...w, paired: false, pairId: null })),
        pairs: [],
        playerId: null,
        log: ['🌸 選擇角色後，點擊任何單身異性展開互動！'],
        chatHistory: {},
        affection: {},
        turn: 0,
        maxTurns: 30,
        gameEnded: false,
        igLikes: {},
        igComments: {},
        endingTriggered: false,
        gossiped: {},
        stamina: 100,
        maxStamina: 100,
        money: 1500,
        actionCost: 20,
        forcedRest: false,
        userPosts: [],
        userAvatar: null,
        igPosts: {},
        unlockedStories: [],
        storyChoices: {},
        diary: [],
        achievements: [],
        voteHistory: [],
        eventsTriggered: [],
        newCharactersAdded: false,
        dailyGoals: [],
        endingCollection: [],
        paradiseVisited: false,
        giftCount: 0,
        rejectCount: 0
    };

    // ✅ 好感度全部從 0 開始
    ALL_CHARS.forEach(c => {
        state.affection[c.id] = 0;
        state.igPosts[c.id] = IG_POSTS_DATA[c.id] || [];
    });

    // ============================================================
    // 輔助函式
    // ============================================================
    function findMan(id) { return state.men.find(m => m.id === id); }
    function findWoman(id) { return state.women.find(w => w.id === id); }
    function findChar(id) { return ALL_CHARS.find(c => c.id === id); }
    function getPairByMan(manId) { return state.pairs.find(p => p.manId === manId); }
    function getPairByWoman(womanId) { return state.pairs.find(p => p.womanId === womanId); }
    function isPlayer(id) { return state.playerId === id; }
    function getPlayer() { if (!state.playerId) return null; return ALL_CHARS.find(c => c.id === state.playerId); }
    function getPartner(id) {
        const char = findChar(id);
        if (!char) return null;
        const isMale = MEN.some(m => m.id === id);
        const pair = isMale ? getPairByMan(id) : getPairByWoman(id);
        if (!pair) return null;
        return isMale ? findWoman(pair.womanId) : findMan(pair.manId);
    }
    function countSingles() { return state.men.filter(m => !m.paired).length + state.women.filter(w => !w.paired).length; }
    function getAffection(id) { return state.affection[id] || 0; }
    function setAffection(id, value) { state.affection[id] = Math.max(0, Math.min(100, value)); }
    function addAffection(id, delta) {
        const current = getAffection(id);
        setAffection(id, current + delta);
        checkStoryTrigger(id);
        checkAchievements();
    }
    function getAllOpponents() {
        const player = getPlayer();
        if (!player) return [];
        const isMale = MEN.some(m => m.id === state.playerId);
        return isMale ? state.women : state.men;
    }
    function getRandomChar(excludeId) {
        const available = ALL_CHARS.filter(c => c.id !== excludeId);
        if (available.length === 0) return null;
        return available[Math.floor(Math.random() * available.length)];
    }
    function hasSecretCrush(charId) {
        for (const c of ALL_CHARS) {
            if (c.id === charId) continue;
            if (getAffection(c.id) > 60 && getPartner(c.id)?.id === charId) {
                return c;
            }
        }
        return null;
    }

    // ============================================================
    // 體力與金錢
    // ============================================================
    function getStamina() { return state.stamina; }
    function setStamina(value) { state.stamina = Math.max(0, Math.min(state.maxStamina, value)); }
    function addStamina(value) { setStamina(getStamina() + value); }
    function getMoney() { return state.money; }
    function setMoney(value) { state.money = Math.max(0, value); }
    function addMoney(value) { setMoney(getMoney() + value); checkAchievements(); }
    function spendMoney(amount) { if (getMoney() < amount) return false; setMoney(getMoney() - amount); return true; }
    function useStamina() { if (getStamina() < state.actionCost) return false; addStamina(-state.actionCost); return true; }

    // ============================================================
    // 成就系統
    // ============================================================
    function unlockAchievement(id) {
        if (state.achievements.includes(id)) return;
        state.achievements.push(id);
        const ach = ACHIEVEMENTS[id];
        if (ach) {
            showAchievementToast(`${ach.icon} ${ach.name}`);
            addLog(`🏆 解鎖成就：${ach.name} - ${ach.desc}`);
            if (id === 'first_story') addMoney(100);
            if (id === 'story_collector') addMoney(200);
            if (id === 'story_master') addMoney(300);
            if (id === 'first_love') addMoney(150);
            if (id === 'popular') addMoney(200);
            if (id === 'rich') addMoney(100);
            if (id === 'helper') addMoney(150);
            if (id === 'perfect') addMoney(300);
            updateUI();
        }
    }

    function checkAchievements() {
        const player = getPlayer();
        if (!player) return;
        const storyCount = state.unlockedStories.length;
        if (storyCount >= 1) unlockAchievement('first_story');
        if (storyCount >= 5) unlockAchievement('story_collector');
        if (storyCount >= 10) unlockAchievement('story_master');
        if (getMoney() >= 3000) unlockAchievement('rich');
        if (state.turn >= 30) unlockAchievement('survivor');
        if ((state.giftCount || 0) >= 10) unlockAchievement('helper');
        if (state.endingTriggered && state.endingType === 'HE') unlockAchievement('perfect');
    }

    function showAchievementToast(text) {
        const toast = document.getElementById('achievementToast');
        toast.textContent = text;
        toast.classList.add('show');
        setTimeout(() => toast.classList.remove('show'), 3000);
    }

    // ============================================================
    // 故事系統
    // ============================================================
    function checkStoryTrigger(charId) {
        const player = getPlayer();
        if (!player) return;
        if (charId === player.id) return;
        const stories = STORIES[charId];
        if (!stories) return;
        const aff = getAffection(charId);
        const char = findChar(charId);
        for (const story of stories) {
            const storyId = `${charId}_${story.chapter}`;
            if (state.unlockedStories.includes(storyId)) continue;
            if (aff >= story.triggerAffection) {
                showStory(char, story, storyId);
                return;
            }
        }
    }

    function showStory(char, story, storyId) {
        const overlay = document.getElementById('storyOverlay');
        document.getElementById('storyAvatar').textContent = char.emoji;
        document.getElementById('storyName').textContent = char.name;
        document.getElementById('storyChapter').textContent = `第 ${['一','二','三'][story.chapter-1]}章 · ${story.title}`;
        document.getElementById('storyDialogue').textContent = story.dialogue;
        const choicesDiv = document.getElementById('storyChoices');
        choicesDiv.innerHTML = '';
        story.choices.forEach((choice, index) => {
            const btn = document.createElement('button');
            const letters = ['A', 'B', 'C'];
            btn.innerHTML = `<span class="choice-tag">${letters[index]}.</span> ${choice.text}`;
            btn.addEventListener('click', function() {
                handleStoryChoice(storyId, choice, story, char);
            });
            choicesDiv.appendChild(btn);
        });
        document.getElementById('storyResult').className = 'story-result';
        document.getElementById('storyResult').textContent = '';
        document.getElementById('storyResult').style.display = 'none';
        const skipBtn = document.getElementById('storySkipBtn');
        skipBtn.onclick = function() {
            overlay.classList.remove('open');
            addLog(`⏭️ 跳過 ${char.name} 的故事：${story.title}`);
        };
        overlay.classList.add('open');
    }

    function handleStoryChoice(storyId, choice, story, char) {
        state.storyChoices[storyId] = choice.text;
        const resultDiv = document.getElementById('storyResult');
        resultDiv.textContent = choice.result;
        resultDiv.className = 'story-result show';
        resultDiv.style.display = 'block';
        addAffection(char.id, choice.affDelta);
        if (!state.unlockedStories.includes(storyId)) {
            state.unlockedStories.push(storyId);
            addDiary(`📖 解鎖 ${char.name} 的故事「${story.title}」`);
            checkAchievements();
        }
        updateUI();
        document.getElementById('storyChoices').style.display = 'none';
        setTimeout(() => {
            document.getElementById('storyOverlay').classList.remove('open');
            document.getElementById('storyChoices').style.display = 'grid';
        }, 2000);
        addLog(`💬 ${char.name} 的故事「${story.title}」已解鎖！`);
    }

    // ============================================================
    // 日記系統
    // ============================================================
    function addDiary(entry) {
        const time = new Date();
        const timeStr = `第${state.turn}回合 ${time.getHours()}:${String(time.getMinutes()).padStart(2,'0')}`;
        state.diary.push(`[${timeStr}] ${entry}`);
        if (state.diary.length > 50) state.diary.shift();
        renderDiary();
    }

    function renderDiary() {
        const container = document.getElementById('diaryContent');
        if (!container) return;
        if (state.diary.length === 0) { container.innerHTML = '📭 還沒有日記記錄，開始你的旅程吧！'; return; }
        container.innerHTML = state.diary.slice(-20).map(d =>
            `<div style="padding:4px 0; border-bottom:1px solid #f0e8e0;">${d}</div>`
        ).join('');
    }

    // ============================================================
    // 排行榜
    // ============================================================
    function renderRanking() {
        const container = document.getElementById('rankingContent');
        if (!container) return;
        const player = getPlayer();
        if (!player) { container.innerHTML = '<div style="text-align:center;color:#9a7a6a;padding:20px 0;">請先選擇角色</div>'; return; }
        const ranked = ALL_CHARS.map(c => ({ ...c, aff: getAffection(c.id), isPlayer: isPlayer(c.id), paired: c.paired }))
            .sort((a, b) => b.aff - a.aff);
        const medals = ['🥇', '🥈', '🥉'];
        container.innerHTML = ranked.map((c, i) => {
            const medal = i < 3 ? medals[i] : `#${i+1}`;
            const medalClass = i === 0 ? 'gold' : i === 1 ? 'silver' : i === 2 ? 'bronze' : '';
            const playerTag = c.isPlayer ? ' 👤' : '';
            const pairedTag = c.paired ? ' 💞' : '';
            return `<div class="rank-item"><span class="rank ${medalClass}">${medal}</span><span class="name">${c.emoji} ${c.name}${playerTag}${pairedTag}</span><span class="aff">❤️ ${c.aff}</span></div>`;
        }).join('');
    }

    // ============================================================
    // 隨機事件
    // ============================================================
    function triggerRandomEvent() {
        if (state.gameEnded || state.endingTriggered) return;
        const events = [
            { name: '🌊 暴風雨來襲', desc: '地獄島突然颳起暴風雨！你全身濕透，體力 -10', effect: function() { addStamina(-10); } },
            { name: '📩 神秘信件', desc: '你收到一封匿名信，裡面寫著一個秘密：某人對你有好感！', effect: function() {
                const target = getRandomChar(state.playerId);
                if (target) { addAffection(target.id, 5); addLog(`💌 秘密信件：${target.emoji} ${target.name} 對你有好感！`); }
            } },
            { name: '🍳 找到食材', desc: '你在海邊發現了一些新鮮食材！金錢 +100', effect: function() { addMoney(100); } },
            { name: '💔 情敵出現', desc: '有人向你喜歡的對象告白！你要介入還是退出？', effect: function() {
                const player = getPlayer();
                if (!player) return;
                const target = getRandomChar(state.playerId);
                if (target && getAffection(target.id) > 50) { addAffection(target.id, -5); addLog(`💔 ${target.emoji} ${target.name} 被告白影響，對你的好感度 -5`); }
            } },
            { name: '🎵 星空音樂會', desc: '今晚星空很美，有人舉辦了即興音樂會！全體好感度 +2', effect: function() {
                ALL_CHARS.forEach(c => { if (c.id !== state.playerId) addAffection(c.id, 2); });
            } }
        ];
        const event = events[Math.floor(Math.random() * events.length)];
        if (event) {
            showEventNotification(event.name, event.desc);
            event.effect();
            addLog(`🌟 隨機事件：${event.name} - ${event.desc}`);
            addDiary(`🌟 ${event.name}：${event.desc}`);
        }
    }

    function showEventNotification(title, desc) {
        const el = document.getElementById('eventNotification');
        el.textContent = `${title} - ${desc}`;
        el.classList.add('show');
        setTimeout(() => el.classList.remove('show'), 4000);
    }

    // ============================================================
    // 命運轉盤
    // ============================================================
    function triggerWheel() {
        if (state.gameEnded || state.endingTriggered) return;
        const results = [
            { name: '❤️ 命運之愛', desc: '某個人的好感度大幅提升！', effect: function() {
                const target = getRandomChar(state.playerId);
                if (target) { addAffection(target.id, 15); addLog(`💖 命運轉盤：${target.emoji} ${target.name} 好感度 +15！`); }
            }, emoji: '❤️' },
            { name: '💰 財運亨通', desc: '獲得大量金錢！', effect: function() { addMoney(300); addLog(`💰 命運轉盤：獲得 300 金錢！`); }, emoji: '💰' },
            { name: '⚡ 體力充沛', desc: '體力完全恢復！', effect: function() { setStamina(100); addLog(`⚡ 命運轉盤：體力完全恢復！`); }, emoji: '⚡' },
            { name: '💔 命運考驗', desc: '某人對你的好感度下降...', effect: function() {
                const target = getRandomChar(state.playerId);
                if (target) { addAffection(target.id, -10); addLog(`💔 命運轉盤：${target.emoji} ${target.name} 好感度 -10！`); }
            }, emoji: '💔' },
            { name: '🌟 人氣爆發', desc: '所有角色對你的好感度 +5！', effect: function() {
                ALL_CHARS.forEach(c => { if (c.id !== state.playerId) addAffection(c.id, 5); });
                addLog(`🌟 命運轉盤：全體好感度 +5！`);
            }, emoji: '🌟' },
            { name: '🎁 神秘禮物', desc: '獲得一份神秘禮物，金錢 +150，隨機好感度 +5', effect: function() {
                addMoney(150);
                const target = getRandomChar(state.playerId);
                if (target) addAffection(target.id, 5);
                addLog(`🎁 命運轉盤：獲得金錢 150 和神秘禮物！`);
            }, emoji: '🎁' }
        ];
        const result = results[Math.floor(Math.random() * results.length)];
        const overlay = document.getElementById('wheelOverlay');
        document.getElementById('wheelSpin').textContent = '🎰';
        document.getElementById('wheelResult').textContent = result.emoji + ' ' + result.name;
        document.getElementById('wheelDesc').textContent = result.desc;
        const spinEl = document.getElementById('wheelSpin');
        spinEl.style.animation = 'none';
        setTimeout(() => { spinEl.style.animation = 'spin 2s ease-in-out'; }, 10);
        overlay.classList.add('open');
        document.getElementById('wheelConfirmBtn').onclick = function() {
            result.effect();
            overlay.classList.remove('open');
            updateUI();
            render();
            addDiary(`🎡 命運轉盤：${result.name}`);
        };
    }

    // ============================================================
    // 人氣投票
    // ============================================================
    function triggerVote() {
        if (state.gameEnded || state.endingTriggered) return;
        const scores = {};
        ALL_CHARS.forEach(c => {
            let total = 0;
            ALL_CHARS.forEach(other => { if (other.id !== c.id) total += getAffection(c.id); });
            scores[c.id] = total;
        });
        let maxScore = 0, winnerId = null;
        for (const [id, score] of Object.entries(scores)) {
            if (score > maxScore) { maxScore = score; winnerId = id; }
        }
        if (winnerId) {
            const winner = findChar(winnerId);
            if (winner) {
                addMoney(200);
                if (winner.id === state.playerId) {
                    addAffection(winner.id, 10);
                    unlockAchievement('popular');
                    addLog(`🌟 人氣投票結果：🎉 你獲得人氣王！獎勵金錢 200，好感度 +10！`);
                    addDiary(`🌟 獲得人氣王！`);
                } else {
                    addAffection(winner.id, 5);
                    addLog(`🌟 人氣投票結果：${winner.emoji} ${winner.name} 獲得人氣王！`);
                    addDiary(`🌟 ${winner.name} 獲得人氣王`);
                }
                state.voteHistory.push({ winner: winnerId, turn: state.turn });
            }
        }
    }

    // ============================================================
    // 天堂島爭奪戰
    // ============================================================
    function triggerParadise() {
        if (state.gameEnded || state.endingTriggered) return;
        let bestPair = null, bestScore = 0;
        for (const pair of state.pairs) {
            const man = findMan(pair.manId);
            const woman = findWoman(pair.womanId);
            if (man && woman) {
                const score = getAffection(man.id) + getAffection(woman.id);
                if (score > bestScore) { bestScore = score; bestPair = { man, woman }; }
            }
        }
        if (bestPair) {
            const { man, woman } = bestPair;
            addAffection(man.id, 15);
            addAffection(woman.id, 15);
            state.paradiseVisited = true;
            addLog(`🏝️ 天堂島爭奪戰：${man.emoji} ${man.name} 和 ${woman.emoji} ${woman.name} 前往天堂島！好感度 +15！`);
            addDiary(`🏝️ ${man.name} 和 ${woman.name} 前往天堂島約會`);
        }
    }

    // ============================================================
    // 新角色加入
    // ============================================================
    function addNewCharacters() {
        if (state.newCharactersAdded) return;
        state.newCharactersAdded = true;
        const newMen = [{ id: 'm7', name: '東旭', emoji: '🦊', personality: '溫暖型', personalityDesc: '溫柔體貼，善於照顧人', paired: false, pairId: null },
            { id: 'm8', name: '在赫', emoji: '🐯', personality: '熱情型', personalityDesc: '充滿活力，總是帶給人歡樂', paired: false, pairId: null }];
        const newWomen = [{ id: 'w7', name: '瑞妍', emoji: '🌺', personality: '直率型', personalityDesc: '有話直說，不做作', paired: false, pairId: null },
            { id: 'w8', name: '智媛', emoji: '🌷', personality: '文靜型', personalityDesc: '溫柔內向，需要慢慢了解', paired: false, pairId: null }];
        state.men = [...state.men, ...newMen];
        state.women = [...state.women, ...newWomen];
        const newAllChars = [...newMen, ...newWomen];
        ALL_CHARS.push(...newAllChars);
        newAllChars.forEach(c => {
            state.affection[c.id] = 0;
            state.igPosts[c.id] = [{ content: `🌟 大家好！我是 ${c.name}，請多多指教！`, time: '剛剛' },
                { content: `🏝️ 剛來到地獄島，有點緊張...`, time: '5分鐘前' }];
        });
        addLog(`🌟 新角色加入：${newAllChars.map(c => c.emoji + c.name).join('、')}！`);
        addDiary(`🌟 新角色加入！`);
        render();
    }

    // ============================================================
    // 結局系統
    // ============================================================
    let endingType = null;

    function checkEnding() {
        if (state.endingTriggered) return true;
        const player = getPlayer();
        if (!player) return false;
        if (state.turn >= state.maxTurns && !player.paired) { triggerEnding('BE'); return true; }
        if (player.paired) {
            const partner = getPartner(player.id);
            if (partner) {
                const aff = getAffection(partner.id);
                if (aff >= 80) { triggerEnding('HE'); return true; }
                else if (aff <= 35) { triggerEnding('BE'); return true; }
            }
        }
        for (const c of ALL_CHARS) {
            if (c.id !== state.playerId) {
                const aff = getAffection(c.id);
                if (aff >= 90) { triggerEnding('OE'); return true; }
            }
        }
        return false;
    }

    function triggerEnding(type) {
        if (state.endingTriggered) return;
        state.endingTriggered = true;
        state.gameEnded = true;
        endingType = type;
        if (!state.endingCollection.includes(type)) state.endingCollection.push(type);
        const overlay = document.getElementById('endingOverlay');
        const icon = document.getElementById('endingIcon');
        const title = document.getElementById('endingTitle');
        const sub = document.getElementById('endingSub');
        document.getElementById('heAudio').pause();
        document.getElementById('beAudio').pause();
        let storySummary = '';
        if (state.unlockedStories.length > 0) {
            storySummary = `\n\n📖 你解鎖了 ${state.unlockedStories.length} 個角色故事：\n${state.unlockedStories.map(id => {
                const parts = id.split('_');
                const char = findChar(parts[0]);
                const chapter = parts[1];
                return `- ${char ? char.emoji + char.name : ''} 第${['一','二','三'][parseInt(chapter)-1]}章`;
            }).join('\n')}`;
        }
        if (type === 'HE') {
            icon.textContent = '💕';
            title.textContent = '♥ 幸福結局 ♥';
            sub.textContent = `告白成功！有情人終成眷屬 ❤️ 你們在節目結束後正式交往，成為令人羨慕的一對！${storySummary}`;
            document.getElementById('heAudio').loop = true;
            document.getElementById('heAudio').play().catch(() => {});
            addLog('🎉 達成幸福結局！');
            unlockAchievement('perfect');
        } else if (type === 'BE') {
            icon.textContent = '💔';
            title.textContent = '♡ 悲傷結局 ♡';
            sub.textContent = `節目結束了，你仍然是單身... 😢 雖然遺憾，但這也是一種成長。${storySummary}`;
            document.getElementById('beAudio').loop = true;
            document.getElementById('beAudio').play().catch(() => {});
            addLog('😢 達成悲傷結局...');
        } else {
            icon.textContent = '🌅';
            title.textContent = '✦ 開放結局 ✦';
            sub.textContent = `在節目中沒有明確表態，但你們在節目外有了更多發展的可能性 🌟 未來充滿無限可能！${storySummary}`;
            addLog('🌅 達成開放結局！');
        }
        overlay.classList.add('open');
        document.getElementById('restBtn').disabled = true;
        updateTurnDisplay();
        render();
    }

    // ============================================================
    // 回合系統
    // ============================================================
    function advanceTurn() {
        if (state.gameEnded || state.endingTriggered) return;
        state.turn++;
        updateTurnDisplay();
        addLog(`🔄 第 ${state.turn} 回合開始`);
        for (const c of ALL_CHARS) {
            if (c.id !== state.playerId) {
                const delta = Math.floor(Math.random() * 6) - 2;
                addAffection(c.id, delta);
            }
        }
        if (state.turn % 5 === 0) { triggerRandomEvent(); triggerVote(); triggerParadise(); }
        if (state.turn % 5 === 0) { setTimeout(() => triggerWheel(), 500); }
        if (state.turn === 10 && !state.newCharactersAdded) { addNewCharacters(); }
        passiveIncome();
        checkEnding();
        if (!state.endingTriggered && state.turn >= state.maxTurns) { triggerEnding('BE'); }
        generateDailyGoals();
        updateUI();
        render();
    }

    function updateTurnDisplay() {
        const display = document.getElementById('turnDisplay');
        display.textContent = `📅 第 ${state.turn} / ${state.maxTurns} 回合`;
        if (state.gameEnded || state.endingTriggered) display.textContent += ' ⏹ 已結束';
    }

    function doRest() {
        if (state.gameEnded || state.endingTriggered) return;
        addStamina(30);
        addLog(`💤 你休息了一回合，恢復 30 體力（當前 ${getStamina()}）`);
        advanceTurn();
    }

    function passiveIncome() {
        if (Math.random() < 0.3) {
            const amount = 50 + Math.floor(Math.random() * 150);
            const sender = getRandomChar(state.playerId);
            if (sender) {
                addMoney(amount);
                addLog(`🎁 ${sender.emoji} ${sender.name} 送了禮物給你！變賣後獲得 💰 ${amount} 金錢`);
            } else {
                addMoney(amount);
                addLog(`🎁 有人送了禮物給你！變賣後獲得 💰 ${amount} 金錢`);
            }
            state.giftCount = (state.giftCount || 0) + 1;
        }
        updateUI();
    }

    function generateDailyGoals() {
        const goals = [
            { text: '💬 和 3 位不同的角色聊天', check: function() { return true; }, reward: 100 },
            { text: '❤️ 送 1 份禮物', check: function() { return true; }, reward: 80 },
            { text: '👀 觀察 2 位角色', check: function() { return true; }, reward: 60 },
            { text: '💌 向 1 位角色告白', check: function() { return true; }, reward: 120 },
            { text: '📢 打聽 2 次消息', check: function() { return true; }, reward: 70 }
        ];
        state.dailyGoals = goals.sort(() => Math.random() - 0.5).slice(0, 3);
    }

    // ============================================================
    // 渲染函式
    // ============================================================
    function renderPlayerSelect() {
        const selectEl = document.getElementById('playerSelect');
        if (!selectEl) return;
        const all = [...state.men, ...state.women];
        selectEl.innerHTML = all.map(c => {
            const active = isPlayer(c.id);
            return `<button class="btn ${active ? 'player-active' : ''}" data-id="${c.id}">${c.emoji} ${c.name} ${active ? '✓' : ''}</button>`;
        }).join('');
        selectEl.querySelectorAll('.btn').forEach(b => {
            b.addEventListener('click', function(e) { e.stopPropagation(); selectPlayer(this.dataset.id); });
        });
    }

    function updateUI() {
        const stamina = getStamina();
        const maxStamina = state.maxStamina;
        const pct = Math.round((stamina / maxStamina) * 100);
        document.getElementById('staminaFill').style.width = pct + '%';
        document.getElementById('staminaText').textContent = `${stamina}/${maxStamina}`;
        document.getElementById('moneyDisplay').textContent = getMoney();
        document.getElementById('myStamina').textContent = stamina;
        document.getElementById('myMoney').textContent = getMoney();
        document.getElementById('myAchievementCount').textContent = state.achievements.length;
        document.getElementById('myStoryCount').textContent = state.unlockedStories.length;

        // ✅ 成就列表
        const achList = document.getElementById('myAchievementList');
        if (achList) {
            if (state.achievements.length === 0) {
                achList.innerHTML = '尚未解鎖任何成就';
            } else {
                achList.innerHTML = state.achievements.map(id => {
                    const ach = ACHIEVEMENTS[id];
                    return ach ? `<div style="padding:2px 0;">${ach.icon} ${ach.name}</div>` : '';
                }).join('');
            }
        }

        const player = getPlayer();
        if (player) {
            document.getElementById('myName').textContent = `${player.emoji} ${player.name}`;
            document.getElementById('myStatus').textContent = player.paired ? '💞 已配對' : '💔 單身';
            const partner = getPartner(player.id);
            document.getElementById('myPartner').textContent = partner ? `${partner.emoji} ${partner.name}` : '尚未配對';
            const avatarEl = document.getElementById('myAvatar');
            if (state.userAvatar) { avatarEl.innerHTML = `<img src="${state.userAvatar}" alt="頭像">`; }
            else { avatarEl.innerHTML = player.emoji; }
        } else {
            document.getElementById('myName').textContent = '未選擇角色';
            document.getElementById('myStatus').textContent = '💔 單身';
            document.getElementById('myPartner').textContent = '尚未配對';
            const avatarEl = document.getElementById('myAvatar');
            if (state.userAvatar) { avatarEl.innerHTML = `<img src="${state.userAvatar}" alt="頭像">`; }
            else { avatarEl.innerHTML = '👤'; }
        }
        renderPlayerSelect();
        renderRanking();
        renderDiary();
    }

    function changeAvatar() { document.getElementById('avatarInput').click(); }
    function handleAvatarUpload(event) {
        const file = event.target.files[0];
        if (!file) return;
        const reader = new FileReader();
        reader.onload = function(e) { state.userAvatar = e.target.result; updateUI(); addLog('🖼️ 頭像已更新！'); };
        reader.readAsDataURL(file);
        event.target.value = '';
    }
    window.changeAvatar = changeAvatar;
    window.handleAvatarUpload = handleAvatarUpload;

    // ============================================================
    // 互動系統
    // ============================================================
    let selectedTarget = null;

    function openInteractModal(targetId) {
        if (state.gameEnded || state.endingTriggered) { addLog('⛔ 遊戲已經結束，無法再互動'); return; }
        const player = getPlayer();
        if (!player) { addLog('💭 請先選擇你的角色！'); return; }
        const target = findChar(targetId);
        if (!target) return;
        if (target.paired) { addLog(`💔 ${target.emoji} ${target.name} 已經配對了，無法互動`); return; }
        if (target.id === state.playerId) { addLog('😅 不能跟自己互動喔'); return; }
        if (getStamina() < state.actionCost) { addLog(`⚡ 體力不足（${getStamina()}/${state.actionCost}），請按「休息」恢復！`); return; }
        selectedTarget = targetId;
        document.getElementById('modalTitle').textContent = `💬 與 ${target.emoji} ${target.name} 互動`;
        const aff = getAffection(targetId);
        document.getElementById('modalSub').textContent = `❤️ 好感度：${aff} | 關係：單身 | ⚡ 體力：${getStamina()}`;
        const confessBtn = document.querySelector('#modalActions button[data-action="confess"]');
        if (aff > 70) confessBtn.textContent = '💕 告白（高機率）';
        else if (aff > 40) confessBtn.textContent = '💌 告白（普通）';
        else confessBtn.textContent = '💌 告白（低機率）';
        const giftBtn = document.querySelector('#modalActions button[data-action="gift"]');
        giftBtn.textContent = `🎁 送禮物 (💰${50 + Math.floor(Math.random() * 100)})`;
        document.getElementById('interactModal').classList.add('open');
    }

    function closeInteractModal() { document.getElementById('interactModal').classList.remove('open'); selectedTarget = null; }

    function handleInteract(action) {
        if (state.gameEnded || state.endingTriggered) { addLog('⛔ 遊戲已經結束'); closeInteractModal(); return; }
        if (!selectedTarget) { closeInteractModal(); return; }
        const target = findChar(selectedTarget);
        const player = getPlayer();
        if (!player || !target) { closeInteractModal(); return; }
        if (getStamina() < state.actionCost) {
            addLog(`⚡ 體力不足（${getStamina()}/${state.actionCost}），請按「休息」恢復！`);
            closeInteractModal(); updateUI(); render(); return;
        }
        addStamina(-state.actionCost);
        const aff = getAffection(target.id);
        let msg = '';
        switch (action) {
            case 'chat': {
                closeInteractModal();
                msg = `💬 你開始與 ${target.emoji} ${target.name} 私下聊天`;
                addAffection(target.id, 3);
                addLog(msg);
                goToPage(1);
                setTimeout(() => { document.querySelector('[data-tab="kakao"]').click(); openChat(target.id); }, 400);
                updateUI(); render(); return;
            }
            case 'confess': {
                const successRate = Math.min(0.9, (aff / 100) * 0.9 + 0.1);
                const success = Math.random() < successRate;
                if (success) {
                    const isMale = MEN.some(m => m.id === state.playerId);
                    const man = isMale ? player : target;
                    const woman = isMale ? target : player;
                    if (!man.paired && !woman.paired) {
                        man.paired = true; man.pairId = woman.id;
                        woman.paired = true; woman.pairId = man.id;
                        state.pairs.push({ manId: man.id, womanId: woman.id });
                        addAffection(target.id, 20);
                        unlockAchievement('first_love');
                        msg = `💌 告白成功！ ${player.emoji} ${player.name} 與 ${target.emoji} ${target.name} 成為情侶 ❤️`;
                        setTimeout(() => checkEnding(), 500);
                    } else { msg = `❌ 告白失敗，其中一人已脫單`; }
                } else {
                    addAffection(target.id, -5);
                    state.rejectCount = (state.rejectCount || 0) + 1;
                    if (state.rejectCount >= 3) unlockAchievement('heart_breaker');
                    msg = `😅 告白被婉拒了... ${target.emoji} ${target.name} 說想再觀察看看。好感度 -5`;
                }
                addLog(msg);
                closeInteractModal();
                updateUI(); render(); return;
            }
            case 'observe': {
                const info = [
                    `${target.emoji} ${target.name} 看起來心情不錯，正在和海邊散步`,
                    `${target.emoji} ${target.name} 一個人坐著發呆，似乎在煩惱什麼`,
                    `${target.emoji} ${target.name} 和其他人聊得很開心，但偶爾會往你這邊看`,
                    `${target.emoji} ${target.name} 正在努力生火，看起來很認真`,
                    `${target.emoji} ${target.name} 似乎對你有些在意，但不敢主動靠近`
                ];
                let observeMsg = info[Math.floor(Math.random() * info.length)];
                const crush = hasSecretCrush(target.id);
                if (crush) { observeMsg += ` 🔍 你發現 ${target.emoji} ${target.name} 好像對 ${crush.emoji} ${crush.name} 特別在意...`; }
                addAffection(target.id, 2);
                msg = `👀 你觀察 ${target.emoji} ${target.name}：${observeMsg} 好感度 +2`;
                addLog(msg);
                closeInteractModal();
                updateUI(); render(); return;
            }
            case 'gift': {
                const cost = 50 + Math.floor(Math.random() * 100);
                if (!spendMoney(cost)) { addLog(`💰 金錢不足！送禮物需要 ${cost}，你只有 ${getMoney()}`); closeInteractModal(); updateUI(); render(); return; }
                state.giftCount = (state.giftCount || 0) + 1;
                const giftMsgs = [
                    `🎁 你花了 💰${cost} 送了一束花給 ${target.emoji} ${target.name}，她/他看起來很開心！好感度 +8`,
                    `🎁 你花了 💰${cost} 準備了親手做的小點心給 ${target.emoji} ${target.name}，對方很感動！好感度 +10`,
                    `🎁 你花了 💰${cost} 送了一條手鍊給 ${target.emoji} ${target.name}，她/他笑著說會好好珍藏！好感度 +7`,
                    `🎁 你花了 💰${cost} 寫了一封信給 ${target.emoji} ${target.name}，對方認真看完後露出了微笑。好感度 +6`
                ];
                addAffection(target.id, 7 + Math.floor(Math.random() * 5));
                msg = giftMsgs[Math.floor(Math.random() * giftMsgs.length)];
                addLog(msg);
                closeInteractModal();
                updateUI(); render(); return;
            }
            case 'gossip': {
                const gossipOptions = [];
                gossipOptions.push(`📢 ${target.emoji} ${target.name} 目前還是單身！`);
                const crush = hasSecretCrush(target.id);
                if (crush) { gossipOptions.push(`📢 聽說 ${target.emoji} ${target.name} 對 ${crush.emoji} ${crush.name} 有好感！`); }
                else {
                    const randomTarget = getRandomChar(target.id);
                    if (randomTarget) { gossipOptions.push(`📢 ${target.emoji} ${target.name} 好像對 ${randomTarget.emoji} ${randomTarget.name} 有點意思...`); }
                }
                const randomGossips = [
                    `📢 有人看到 ${target.emoji} ${target.name} 昨天偷偷寫了封信，不知道要給誰...`,
                    `📢 ${target.emoji} ${target.name} 最近常常一個人發呆，好像在煩惱感情的事`,
                    `📢 聽說 ${target.emoji} ${target.name} 對某個人一見鍾情，但不敢主動表白`,
                    `📢 ${target.emoji} ${target.name} 昨天跟別人聊了很久，但內容沒人聽到`
                ];
                gossipOptions.push(randomGossips[Math.floor(Math.random() * randomGossips.length)]);
                const finalGossip = gossipOptions[Math.floor(Math.random() * gossipOptions.length)];
                msg = finalGossip;
                addLog(msg);
                closeInteractModal();
                updateUI(); render(); return;
            }
            default: { addLog('⚠️ 未知的動作'); closeInteractModal(); updateUI(); render(); }
        }
    }

    // ============================================================
    // 渲染函式
    // ============================================================
    function render() {
        document.getElementById('menContainer').innerHTML = state.men.map(m => {
            const paired = m.paired;
            const pair = getPairByMan(m.id);
            const partner = pair ? findWoman(pair.womanId) : null;
            const tag = paired ? `💞 ${partner ? partner.name : '?'}` : '';
            const pc = isPlayer(m.id) ? 'player' : '';
            const badge = isPlayer(m.id) ? '<span class="badge">你</span>' : '';
            const aff = getAffection(m.id);
            const heart = aff > 60 ? '❤️' : aff > 35 ? '💗' : '🤍';
            const suspicion = paired && !isPlayer(m.id) ? ' ❓' : '';
            const clickable = !paired && !isPlayer(m.id) && !state.gameEnded ? `onclick="window.openInteractModal('${m.id}')"` :
                (paired && !isPlayer(m.id) ? `onclick="window.openInteractModal('${m.id}')"` : '');
            const disabled = paired && !isPlayer(m.id) ? 'paired' : '';
            return `<span class="avatar ${disabled} ${pc}" ${clickable}>
                ${m.emoji} ${m.name} ${badge}
                <span class="heart-icon">${heart}${aff}</span>
                ${tag ? `<span style="font-size:0.55rem;opacity:0.6;">${tag}</span>` : ''}
                ${suspicion ? `<span class="suspicion">❓</span>` : ''}
            </span>`;
        }).join('');

        document.getElementById('womenContainer').innerHTML = state.women.map(w => {
            const paired = w.paired;
            const pair = getPairByWoman(w.id);
            const partner = pair ? findMan(pair.manId) : null;
            const tag = paired ? `💞 ${partner ? partner.name : '?'}` : '';
            const pc = isPlayer(w.id) ? 'player' : '';
            const badge = isPlayer(w.id) ? '<span class="badge">你</span>' : '';
            const aff = getAffection(w.id);
            const heart = aff > 60 ? '❤️' : aff > 35 ? '💗' : '🤍';
            const suspicion = paired && !isPlayer(w.id) ? ' ❓' : '';
            const clickable = !paired && !isPlayer(w.id) && !state.gameEnded ? `onclick="window.openInteractModal('${w.id}')"` :
                (paired && !isPlayer(w.id) ? `onclick="window.openInteractModal('${w.id}')"` : '');
            const disabled = paired && !isPlayer(w.id) ? 'paired' : '';
            return `<span class="avatar ${disabled} ${pc}" ${clickable}>
                ${w.emoji} ${w.name} ${badge}
                <span class="heart-icon">${heart}${aff}</span>
                ${tag ? `<span style="font-size:0.55rem;opacity:0.6;">${tag}</span>` : ''}
                ${suspicion ? `<span class="suspicion">❓</span>` : ''}
            </span>`;
        }).join('');

        document.getElementById('remainingCount').textContent = countSingles();
        document.getElementById('pairCount').textContent = state.pairs.length;

        const player = getPlayer();
        document.getElementById('playerStatus').textContent = player ? `${player.emoji} ${player.name} ${player.paired ? '💞已配對' : '💔單身'}` :
            '未選擇';

        const latest = state.log.slice(-6);
        document.getElementById('logArea').innerHTML = latest.map(msg =>
            `<div class="log-line">${msg}</div>`
        ).join('');

        renderPlayerSelect();
        renderChatList();
        renderInstagram();
        renderRanking();
        renderDiary();
        updateTurnDisplay();
        updateUI();
        document.getElementById('restBtn').disabled = state.gameEnded || state.endingTriggered;
    }

    // ============================================================
    // 聊天列表
    // ============================================================
    function renderChatList() {
        const player = getPlayer();
        if (!player) {
            document.getElementById('chatList').innerHTML =
                '<div style="text-align:center;color:#9a7a6a;padding:30px 0;font-size:0.85rem;">請先選擇角色才能使用手機通訊 📱</div>';
            return;
        }
        const opponents = getAllOpponents();
        const list = document.getElementById('chatList');
        list.innerHTML = opponents.map(o => {
            const history = state.chatHistory[o.id] || [];
            const lastMsg = history.length > 0 ? history[history.length - 1].text : '還沒有對話紀錄';
            const time = history.length > 0 ? history[history.length - 1].time : '';
            const aff = getAffection(o.id);
            const pairedStatus = o.paired ? '🔒' : '💔';
            return `<div class="chat-item" data-id="${o.id}">
                <div class="avatar-chat">${o.emoji}</div>
                <div class="info">
                    <div class="name">${o.name} ${pairedStatus} <span class="affection">❤️${aff}</span></div>
                    <div class="last-msg">${lastMsg}</div>
                </div>
                <div class="info time">${time}</div>
            </div>`;
        }).join('');
        list.querySelectorAll('.chat-item').forEach(item => {
            item.addEventListener('click', function() { if (!state.gameEnded) openChat(this.dataset.id);
                else addLog('⛔ 遊戲已結束'); });
        });
    }

    // ============================================================
    // Instagram
    // ============================================================
    function renderInstagram() {
        const player = getPlayer();
        if (!player) {
            document.getElementById('igContent').innerHTML =
                '<div style="text-align:center;color:#9a7a6a;padding:30px 0;font-size:0.85rem;">請先選擇角色才能查看 Instagram 📸</div>';
            return;
        }
        let allPosts = [];
        for (const c of ALL_CHARS) {
            const posts = state.igPosts[c.id] || [];
            for (const p of posts) {
                allPosts.push({ id: `${c.id}_${Date.now()}_${Math.random()}`, char: c, content: p.content, time: p.time,
                    isUserPost: false });
            }
        }
        for (const p of state.userPosts) {
            allPosts.push({ id: `user_${Date.now()}_${Math.random()}`, char: player, content: p.content, time: p.time ||
                    '剛剛', isUserPost: true });
        }
        allPosts.sort((a, b) => {
            const timeOrder = { '剛剛': 0, '1分鐘前': 1, '5分鐘前': 2, '10分鐘前': 3, '30分鐘前': 4, '1小時前': 5, '2小時前': 6,
                '3小時前': 7, '4小時前': 8, '5小時前': 9, '昨天': 10, '2天前': 11, '3天前': 12, '4天前': 13, '5天前': 14,
                '6天前': 15, '1週前': 16 };
            return (timeOrder[a.time] || 99) - (timeOrder[b.time] || 99);
        });
        const displayPosts = allPosts.slice(0, 20);
        const igContent = document.getElementById('igContent');
        let html = `
            <div class="ig-profile">
                <div class="ig-avatar">${player.emoji}</div>
                <div class="ig-name">@${player.name}_official</div>
                <div class="ig-bio">${player.personality} · 地獄島參賽者 ✨</div>
                <div class="ig-stats">
                    <span><strong>${Math.floor(Math.random() * 5000 + 1000)}</strong> 追蹤</span>
                    <span><strong>${Math.floor(Math.random() * 300 + 50) + state.userPosts.length}</strong> 貼文</span>
                </div>
            </div>
            <div class="ig-post-area">
                <textarea id="igPostInput" placeholder="寫下你的心情... #單身即地獄" rows="2"></textarea>
                <div class="post-btn-row">
                    <button onclick="window.postIG()" class="btn-primary">📤 發文</button>
                </div>
            </div>
            <div class="ig-posts">`;
        for (const p of displayPosts) {
            const postId = `post_${p.id}`;
            const liked = state.igLikes[postId] || false;
            const comments = state.igComments[postId] || [];
            const isMine = p.isUserPost;
            html += `
                <div class="ig-post">
                    <div class="post-header">
                        <div class="post-avatar">${p.char.emoji}</div>
                        <div class="post-name" onclick="window.openChatFromIG('${p.char.id}')">
                            ${p.char.name}_official
                            ${isMine ? '<span class="mine">我的</span>' : ''}
                        </div>
                        <div class="post-time">${p.time}</div>
                    </div>
                    <div class="post-content">${p.content}</div>
                    <div class="post-actions">
                        <button class="${liked ? 'liked' : ''}" onclick="window.toggleLike('${postId}')">❤️ ${liked ? '取消讚' : '按讚'} (${liked ? '1' : '0'})</button>
                        <button onclick="window.toggleComment('${postId}')">💬 留言</button>
                    </div>
                    <div class="comments" id="comments_${postId}">
                        ${comments.map(c => `<div class="comment"><strong>${c.user}:</strong> ${c.text}</div>`).join('')}
                    </div>
                    <div class="comment-area" id="commentArea_${postId}" style="display:none;">
                        <input type="text" id="commentInput_${postId}" placeholder="寫下留言..." maxlength="50">
                        <button onclick="window.submitComment('${postId}')">發送</button>
                    </div>
                </div>`;
        }
        html += `</div>`;
        igContent.innerHTML = html;

        window.postIG = function() {
            if (state.gameEnded) { addLog('⛔ 遊戲已結束'); return; }
            const input = document.getElementById('igPostInput');
            const text = input.value.trim();
            if (!text) { addLog('📝 請輸入貼文內容'); return; }
            state.userPosts.push({ content: text, time: '剛剛' });
            input.value = '';
            addLog(`📸 你發布了一則 IG 貼文：${text}`);
            renderInstagram();
        };
        window.toggleLike = function(postId) {
            if (state.gameEnded) { addLog('⛔ 遊戲已結束'); return; }
            state.igLikes[postId] = !state.igLikes[postId];
            renderInstagram();
        };
        window.toggleComment = function(postId) {
            if (state.gameEnded) { addLog('⛔ 遊戲已結束'); return; }
            const area = document.getElementById(`commentArea_${postId}`);
            if (area) {
                area.style.display = area.style.display === 'none' ? 'flex' : 'none';
                if (area.style.display === 'flex') {
                    const input = document.getElementById(`commentInput_${postId}`);
                    if (input) setTimeout(() => input.focus(), 300);
                }
            }
        };
        window.submitComment = function(postId) {
            if (state.gameEnded) { addLog('⛔ 遊戲已結束'); return; }
            const input = document.getElementById(`commentInput_${postId}`);
            if (!input) return;
            const text = input.value.trim();
            if (!text) return;
            if (!state.igComments[postId]) state.igComments[postId] = [];
            const player = getPlayer();
            state.igComments[postId].push({ user: player ? player.name : '匿名', text: text });
            input.value = '';
            renderInstagram();
            addLog(`💬 你在 IG 留言：${text}`);
        };
        window.openChatFromIG = function(charId) {
            if (state.gameEnded) { addLog('⛔ 遊戲已結束'); return; }
            const char = findChar(charId);
            if (!char) return;
            if (char.id === state.playerId) { addLog('😅 這是你的帳號'); return; }
            goToPage(1);
            setTimeout(() => { document.querySelector('[data-tab="kakao"]').click(); openChat(charId); }, 400);
        };
    }

    // ============================================================
    // 聊天功能
    // ============================================================
    let currentChatPartner = null;

    function openChat(partnerId) {
        if (state.gameEnded || state.endingTriggered) { addLog('⛔ 遊戲已結束'); return; }
        const partner = findChar(partnerId);
        if (!partner) return;
        currentChatPartner = partnerId;
        if (!state.chatHistory[partnerId]) {
            state.chatHistory[partnerId] = [];
            state.chatHistory[partnerId].push({ text: `안녕하세요~ 我是 ${partner.emoji} ${partner.name}！`, sender: 'received',
                time: getTime() });
            state.chatHistory[partnerId].push({ text: `（${partner.personality}）${partner.personalityDesc}`, sender: 'received',
                time: getTime() });
        }
        document.getElementById('chatWindow').classList.add('open');
        document.getElementById('swipeNav').classList.add('hidden');
        document.getElementById('turnDisplay').style.display = 'none';
        document.getElementById('chatPartnerName').textContent = `${partner.emoji} ${partner.name}`;
        document.getElementById('chatPartnerStatus').textContent = partner.paired ? '💞 配對中' : '💔 單身';
        renderChatMessages(partnerId);
        setTimeout(() => document.getElementById('chatInput').focus(), 300);
    }

    function renderChatMessages(partnerId) {
        const messages = state.chatHistory[partnerId] || [];
        const container = document.getElementById('chatMessages');
        container.innerHTML = messages.map(msg => {
            const isSent = msg.sender === 'sent';
            return `<div class="msg ${isSent ? 'sent' : 'received'}">
                ${msg.text}
                <span class="time-tag">${msg.time} ${isSent ? '✓' : ''}</span>
            </div>`;
        }).join('');
        container.scrollTop = container.scrollHeight;
    }

    function getTime() {
        const now = new Date();
        return String(now.getHours()).padStart(2, '0') + ':' + String(now.getMinutes()).padStart(2, '0');
    }

    function sendMessage() {
        if (state.gameEnded || state.endingTriggered) { addLog('⛔ 遊戲已結束'); return; }
        const input = document.getElementById('chatInput');
        const msg = input.value.trim();
        if (!msg || !currentChatPartner) return;
        const partnerId = currentChatPartner;
        const partner = findChar(partnerId);
        state.chatHistory[partnerId].push({ text: msg, sender: 'sent', time: getTime() });
        renderChatMessages(partnerId);
        input.value = '';
        addAffection(partnerId, 1);
        const container = document.getElementById('chatMessages');
        const typingDiv = document.createElement('div');
        typingDiv.className = 'typing-indicator';
        typingDiv.innerHTML = `${partner.emoji} 正在輸入 <span class="dot">•</span><span class="dot">•</span><span class="dot">•</span>`;
        container.appendChild(typingDiv);
        container.scrollTop = container.scrollHeight;
        const delay = Math.random() * 1500 + 1200;
        setTimeout(() => {
            const typing = container.querySelector('.typing-indicator');
            if (typing) typing.remove();
            const response = generateSmartResponse(partnerId, msg);
            state.chatHistory[partnerId].push({ text: response, sender: 'received', time: getTime() });
            renderChatMessages(partnerId);
            render();
        }, delay);
    }

    function generateSmartResponse(partnerId, playerMsg) {
        const partner = findChar(partnerId);
        if (!partner) return '...';
        const isPaired = partner.paired;
        const isPartnerWithPlayer = isPaired && getPartner(partnerId)?.id === state.playerId;
        const affection = getAffection(partnerId);
        const msg = playerMsg.toLowerCase();
        const personality = partner.personality || '溫暖型';
        const type = {
            '熱情型': {
                greeting: [
                    `안녕~ ${isPartnerWithPlayer ? '寶貝！' : ''}今天過得好嗎？😊💕`,
                    `嗨！${isPartnerWithPlayer ? '我正想找你呢 💕' : '很高興認識你！'}`,
                    `你好呀～ ${isPartnerWithPlayer ? '等你好久了 ❤️' : '一起加油吧！'}`,
                    `Hi！${isPartnerWithPlayer ? '你終於來了！' : '你的笑容好迷人 😊'}`
                ],
                love: [
                    `我也想你 ❤️ 你不在的時候我好無聊！`,
                    `真的嗎？我好開心 😊💕 我也很喜歡你！`,
                    `你終於說出來了！我等你這句話等好久 😍`,
                    `我喜歡你！不，我超喜歡你！❤️`
                ],
                default: [
                    `你說話真的好有趣 💕 我喜歡跟你聊天！`,
                    `你怎麼總是能讓我心動 💕 我好喜歡你！`,
                    `跟你聊天是我一天中最開心的事 ❤️`
                ]
            },
            '溫暖型': {
                greeting: [
                    `你好 ${isPartnerWithPlayer ? '親愛的 😊' : ''}，今天過得怎麼樣？`,
                    `嗨～ ${isPartnerWithPlayer ? '謝謝你來找我 💕' : '歡迎你！'}`,
                    `안녕하세요~ ${isPartnerWithPlayer ? '我一直在等你訊息 😊' : '請多指教'}`,
                    `你好！${isPartnerWithPlayer ? '今天天氣很好，心情也不錯 💕' : '一起在地獄島加油吧！'}`
                ],
                love: [
                    `我也想你 ❤️ 什麼時候可以再見面？`,
                    `真的嗎？我好開心 😊💕 我也有同樣的感覺。`,
                    `我感受到了你的真心... 我也是。`,
                    `你總是能讓我心裡暖暖的 😊 謝謝你。`
                ],
                default: [
                    `跟你聊天很開心 😊 你總是能讓我微笑`,
                    `感覺跟你在一起很舒服 💕 謝謝你陪我。`,
                    `你是一個很特別的人 ❤️ 我很珍惜你。`
                ]
            },
            '幽默型': {
                greeting: [
                    `嗨！${isPartnerWithPlayer ? '我剛剛還在想你是不是迷路了 😂' : '你終於來了！'}`,
                    `哈囉～ ${isPartnerWithPlayer ? '寶貝今天又更美了 💕' : '你長得好像我未來女朋友/男朋友 😏'}`,
                    `Yo！${isPartnerWithPlayer ? '今天有沒有想我？' : '地獄島有你變得好玩多了！'}`,
                    `早安！${isPartnerWithPlayer ? '昨天夢到你，今天就看到你，我運氣真好 😆' : '今天也要一起加油喔！'}`
                ],
                love: [
                    `我也想你！我剛剛還在想你是不是也在想我 😏`,
                    `哇～ 你這麼直接，我害羞了 😳 好啦我也是！`,
                    `真的嗎？我不信！除非你證明給我看 😤`,
                    `我喜歡你！比喜歡炸雞還喜歡！🍗`
                ],
                default: [
                    `你真的很會說話 💕 我好喜歡跟你聊天！`,
                    `跟你說話真的好開心～ 你是我在這裡最喜歡的人 ❤️`,
                    `你說話的方式好迷人 💕 我好喜歡跟你聊天！`
                ]
            },
            '高冷型': {
                greeting: [
                    `...嗨。`,
                    `嗯。你好。`,
                    `嗨，${isPartnerWithPlayer ? '今天還行。' : ''}`,
                    `你好。${isPartnerWithPlayer ? '你最近很忙？' : ''}`
                ],
                love: [
                    `...我也想你。`,
                    `嗯。我知道了。我也是。`,
                    `......我不常說這種話，但...我也是。`,
                    `...謝謝你告訴我。我也是。`
                ],
                default: [
                    `...嗯。`,
                    `...知道了。`,
                    `...你說的對。`
                ]
            },
            '文靜型': {
                greeting: [
                    `你...你好 😊 ${isPartnerWithPlayer ? '謝謝你來找我...' : ''}`,
                    `嗨... ${isPartnerWithPlayer ? '我一直在等你...' : '很高興認識你...'}`,
                    `你好... ${isPartnerWithPlayer ? '你今天過得好嗎？' : '請多多指教...'}`
                ],
                love: [
                    `你...你也是嗎？😊 我好開心...`,
                    `我...我也想你...但是我不敢說...😊`,
                    `你這麼說...我好感動...😊 我也是...`,
                    `我...我一直在等你說這句話...`
                ],
                default: [
                    `嗯...嗯嗯 😊`,
                    `原來...是這樣啊...`,
                    `你說得...很有道理...😊`
                ]
            },
            '直率型': {
                greeting: [
                    `嗨！${isPartnerWithPlayer ? '我喜歡你，直接說了 😤' : '你長得真好看！'}`,
                    `你好！${isPartnerWithPlayer ? '我今天心情超好因為看到你 💕' : '我們來聊天吧！'}`,
                    `哈囉！${isPartnerWithPlayer ? '你有沒有想我？直接回答！' : '我覺得你很有趣！'}`
                ],
                love: [
                    `我！也！是！你終於說了！😤`,
                    `真的嗎？太好了！我也喜歡你！💕`,
                    `我早就想說了！我喜歡你！❤️`,
                    `我也想你！以後要每天說！`
                ],
                default: [
                    `跟你說話很開心！`,
                    `你真的很不錯！我喜歡！`,
                    `你說的對！我同意！`
                ]
            }
        } [personality] || type['溫暖型'];

        if (msg.includes('你好') || msg.includes('嗨') || msg.includes('hi') || msg.includes('안녕') || msg.includes('哈囉'))
            return type.greeting[Math.floor(Math.random() * type.greeting.length)];
        if (msg.includes('喜歡') || msg.includes('想念') || msg.includes('想你') || msg.includes('愛你'))
            return type.love[Math.floor(Math.random() * type.love.length)];
        if (msg.includes('謝謝') || msg.includes('感謝')) return '不客氣 😊 你值得！';
        if (msg.includes('晚安') || msg.includes('再見') || msg.includes('掰') || msg.includes('bye')) {
            const bye = ['晚安 💕 明天見！', '掰掰～ 我會想你的 😊', '再見～ 謝謝你今天陪我 ❤️'];
            return bye[Math.floor(Math.random() * bye.length)];
        }
        return type.default[Math.floor(Math.random() * type.default.length)];
    }

    // ============================================================
    // 玩家選擇
    // ============================================================
    function selectPlayer(id) {
        if (state.gameEnded || state.endingTriggered) { addLog('⛔ 遊戲已經結束'); return; }
        const char = findChar(id);
        if (!char) return;
        if (state.playerId === id) { addLog(`👤 你已是 ${char.emoji} ${char.name}`); return; }
        state.playerId = id;
        addLog(`🎀 你現在扮演 ${char.emoji} ${char.name} ✦`);
        checkStoryTrigger(id);
        render();
    }

    // ============================================================
    // 重置與存檔
    // ============================================================
    function resetGame() {
        document.getElementById('heAudio').pause();
        document.getElementById('beAudio').pause();
        state.men = MEN.map(m => ({ ...m, paired: false, pairId: null }));
        state.women = WOMEN.map(w => ({ ...w, paired: false, pairId: null }));
        state.pairs = [];
        state.playerId = null;
        state.log = ['🔄 重啟命運，一切歸零 ✦'];
        state.chatHistory = {};
        state.turn = 0;
        state.gameEnded = false;
        state.endingTriggered = false;
        state.igLikes = {};
        state.igComments = {};
        state.gossiped = {};
        state.stamina = 100;
        state.money = 1500;
        state.forcedRest = false;
        state.userPosts = [];
        state.unlockedStories = [];
        state.storyChoices = {};
        state.diary = [];
        state.achievements = [];
        state.voteHistory = [];
        state.eventsTriggered = [];
        state.newCharactersAdded = false;
        state.paradiseVisited = false;
        state.endingCollection = [];
        state.giftCount = 0;
        state.rejectCount = 0;
        endingType = null;
        ALL_CHARS.forEach(c => {
            state.affection[c.id] = 0;
            state.igPosts[c.id] = IG_POSTS_DATA[c.id] || [];
        });
        document.getElementById('chatWindow').classList.remove('open');
        document.getElementById('swipeNav').classList.remove('hidden');
        document.getElementById('endingOverlay').classList.remove('open');
        document.getElementById('restBtn').disabled = false;
        document.getElementById('turnDisplay').style.display = 'block';
        currentChatPartner = null;
        updateTurnDisplay();
        render();
        addLog('🔄 命運重啟！');
    }

    function saveGame() {
        try {
            const saveData = {
                men: state.men,
                women: state.women,
                pairs: state.pairs,
                playerId: state.playerId,
                affection: state.affection,
                turn: state.turn,
                chatHistory: state.chatHistory,
                igLikes: state.igLikes,
                igComments: state.igComments,
                gossiped: state.gossiped,
                stamina: state.stamina,
                money: state.money,
                userPosts: state.userPosts,
                userAvatar: state.userAvatar,
                unlockedStories: state.unlockedStories,
                storyChoices: state.storyChoices,
                diary: state.diary,
                achievements: state.achievements,
                gameEnded: state.gameEnded,
                endingTriggered: state.endingTriggered,
                endingCollection: state.endingCollection,
                giftCount: state.giftCount,
                rejectCount: state.rejectCount,
                paradiseVisited: state.paradiseVisited,
                log: state.log.slice(-10)
            };
            localStorage.setItem('singleHellSave', JSON.stringify(saveData));
            addLog('💾 遊戲已存檔！');
        } catch (e) { addLog('⚠️ 存檔失敗'); }
    }

    function loadGame() {
        try {
            const data = localStorage.getItem('singleHellSave');
            if (!data) { addLog('⚠️ 沒有找到存檔'); return; }
            const save = JSON.parse(data);
            state.men = save.men;
            state.women = save.women;
            state.pairs = save.pairs;
            state.playerId = save.playerId;
            state.affection = save.affection;
            state.turn = save.turn;
            state.chatHistory = save.chatHistory || {};
            state.igLikes = save.igLikes || {};
            state.igComments = save.igComments || {};
            state.gossiped = save.gossiped || {};
            state.stamina = save.stamina !== undefined ? save.stamina : 100;
            state.money = save.money !== undefined ? save.money : 1500;
            state.userPosts = save.userPosts || [];
            state.userAvatar = save.userAvatar || null;
            state.unlockedStories = save.unlockedStories || [];
            state.storyChoices = save.storyChoices || {};
            state.diary = save.diary || [];
            state.achievements = save.achievements || [];
            state.gameEnded = save.gameEnded || false;
            state.endingTriggered = save.endingTriggered || false;
            state.endingCollection = save.endingCollection || [];
            state.giftCount = save.giftCount || 0;
            state.rejectCount = save.rejectCount || 0;
            state.paradiseVisited = save.paradiseVisited || false;
            state.log = save.log || ['📂 讀取存檔成功！'];
            document.getElementById('chatWindow').classList.remove('open');
            document.getElementById('swipeNav').classList.remove('hidden');
            document.getElementById('endingOverlay').classList.remove('open');
            document.getElementById('restBtn').disabled = state.gameEnded || state.endingTriggered;
            document.getElementById('turnDisplay').style.display = 'block';
            currentChatPartner = null;
            updateTurnDisplay();
            render();
            addLog('📂 讀取存檔成功！');
        } catch (e) { addLog('⚠️ 讀取存檔失敗'); }
    }

    function addLog(msg) {
        state.log.push(msg);
        if (state.log.length > 20) state.log.shift();
        const logArea = document.getElementById('logArea');
        if (logArea) {
            const latest = state.log.slice(-6);
            logArea.innerHTML = latest.map(m => `<div class="log-line">${m}</div>`).join('');
        }
        updateUI();
    }

    function clearLog() {
        if (state.log.length > 1) {
            state.log = [state.log[state.log.length - 1]];
            const logArea = document.getElementById('logArea');
            if (logArea) logArea.innerHTML = `<div class="log-line">${state.log[0]}</div>`;
        } else addLog('🗑️ 日誌已清空');
    }

    // ============================================================
    // 滑動控制
    // ============================================================
    const container = document.getElementById('swipeContainer');
    const navBtns = document.querySelectorAll('.swipe-nav button');

    function goToPage(index) {
        container.scrollTo({ left: index * container.offsetWidth, behavior: 'smooth' });
        navBtns.forEach((b, i) => b.classList.toggle('active', i === index));
    }
    window.goToPage = goToPage;
    navBtns.forEach((btn, idx) => { btn.addEventListener('click', () => goToPage(idx)); });
    container.addEventListener('scroll', () => {
        const index = Math.round(container.scrollLeft / container.offsetWidth);
        navBtns.forEach((b, i) => b.classList.toggle('active', i === index));
    });

    // ============================================================
    // 手機頁籤切換
    // ============================================================
    document.querySelectorAll('.tab-btn-phone').forEach(btn => {
        btn.addEventListener('click', function() {
            document.querySelectorAll('.tab-btn-phone').forEach(b => b.classList.remove('active'));
            this.classList.add('active');
            const tab = this.dataset.tab;
            document.getElementById('kakaoTab').style.display = tab === 'kakao' ? 'block' : 'none';
            document.getElementById('instagramTab').style.display = tab === 'instagram' ? 'block' : 'none';
            document.getElementById('rankingTab').style.display = tab === 'ranking' ? 'block' : 'none';
            document.getElementById('diaryTab').style.display = tab === 'diary' ? 'block' : 'none';
            if (tab === 'ranking') renderRanking();
            if (tab === 'diary') renderDiary();
            if (tab === 'instagram') renderInstagram();
        });
    });

    // ============================================================
    // 事件綁定
    // ============================================================
    document.getElementById('modalClose').addEventListener('click', closeInteractModal);
    document.querySelectorAll('#modalActions button').forEach(btn => {
        btn.addEventListener('click', function() { handleInteract(this.dataset.action); });
    });
    document.addEventListener('click', function(e) {
        const modal = document.getElementById('interactModal');
        if (modal.classList.contains('open')) {
            if (!modal.contains(e.target) && !e.target.closest('.avatar')) closeInteractModal();
        }
    });
    window.openInteractModal = openInteractModal;

    document.getElementById('clearPlayerBtn').addEventListener('click', function() {
        if (state.playerId) {
            const p = getPlayer();
            addLog(`🚫 取消扮演 ${p ? p.emoji + ' ' + p.name : ''}`);
            state.playerId = null;
            render();
        } else addLog('💭 你還沒有扮演任何角色');
    });
    document.getElementById('resetBtn').addEventListener('click', resetGame);
    document.getElementById('clearLogBtn').addEventListener('click', clearLog);
    document.getElementById('restBtn').addEventListener('click', doRest);
    document.getElementById('myRestBtn').addEventListener('click', doRest);
    document.getElementById('mySaveBtn').addEventListener('click', saveGame);

    document.getElementById('chatBackBtn').addEventListener('click', function() {
        document.getElementById('chatWindow').classList.remove('open');
        document.getElementById('swipeNav').classList.remove('hidden');
        document.getElementById('turnDisplay').style.display = 'block';
        currentChatPartner = null;
        renderChatList();
    });
    document.getElementById('chatSendBtn').addEventListener('click', sendMessage);
    document.getElementById('chatInput').addEventListener('keydown', function(e) { if (e.key === 'Enter') sendMessage(); });
    document.getElementById('chatInput').addEventListener('focus', function() {
        setTimeout(() => {
            const container = document.getElementById('chatMessages');
            container.scrollTop = container.scrollHeight;
        }, 300);
    });
    document.getElementById('endingSaveBtn').addEventListener('click', saveGame);
    document.getElementById('endingRestartBtn').addEventListener('click', resetGame);

    // ============================================================
    // 啟動
    // ============================================================
    if (localStorage.getItem('singleHellSave')) {
        loadGame();
    } else {
        updateTurnDisplay();
        generateDailyGoals();
        render();
    }
})();
</script>
</body>
</html>