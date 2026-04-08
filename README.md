import React, { useMemo, useState } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { ArrowRight, BookOpen, GraduationCap, FileText, Phone, Mail, ExternalLink, CheckCircle2, Sparkles, Clock3, Users, Monitor, ChevronDown, Home, BriefcaseBusiness, Globe, MessageCircle } from "lucide-react";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Badge } from "@/components/ui/badge";
import { Separator } from "@/components/ui/separator";

const links = {
  teacherProof: "https://drive.google.com/file/d/1MvlW_0s-TeuQgTzOzVmJv71KKCmMKTws/view?usp=drive_link",
  teacherFeedback: "https://drive.google.com/drive/folders/1QN7KNDrU3jZjKkefp59BT2u_lJZDNYYV?usp=sharing",
  level1Record: "https://drive.google.com/drive/folders/1Kz18uO_Lh8mhdGBURhxEe_9iZ9jwDoUN?usp=drive_link",
  level1LessonSamples: "https://drive.google.com/drive/folders/1Klcs9Vcdu-OlIOB2ReH348SGCMuWE_8E?usp=drive_link",
  level1WritingSamples: "https://drive.google.com/drive/folders/1FnfuwtX_I9lErUuMv4CL0rY5Kip4J_Sq?usp=drive_link",
  level2Record: "https://drive.google.com/drive/folders/1nNazAVS97w_QomzMs8eoaxrjzRMgt2VP?usp=drive_link",
  level2LessonSamples: "https://drive.google.com/drive/folders/1Rh0obLAGkTYTAR8ddnUKsuRtHjazHD54?usp=drive_link",
  level2WritingSamples: "https://drive.google.com/drive/folders/16SsDHj5R55RloOJcG8M0X_YT8ogJzoQ7BH?usp=sharing",
  efset: "https://www.efset.org/quick-check/",
  facebook: "https://facebook.com/gianguyendayy",
  fanpage: "https://facebook.com/thelanguage.town",
  instagram: "https://instagram.com/thelanguagetown",
  threads: "https://threads.net/@gnsdeeead",
};

const teacher = {
  name: "Trần Gia Nguyễn (Gin)",
  headline: "8.0 IELTS Overall x5 • R9 | L8.5 | S8.5 | W8.5",
  shortBio:
    "Giáo viên tự do toàn thời gian, người quản lí nội dung ở The Language Town, vận hành các lớp học tiếng Anh với mô hình nhỏ gọn để hỗ trợ học viên sát sao hơn.",
  achievements: [
    "8.0 IELTS x4 - Điểm thành phần cao nhất qua 6 lần thi (8.5L | 9R | 8.5S | 8.5W).",
    "Tốt nghiệp loại giỏi ngành Ngôn ngữ Anh - chuyên ngành sư phạm.",
    "5 năm kinh nghiệm giảng dạy tiếng Anh cho người đi làm, giảng dạy tiếng Anh giao tiếp, và luyện thi IELTS.",
    "Giải ba học sinh giỏi tiếng Anh cấp tỉnh 2017.",
  ],
  contact: {
    phone: "0946316141",
    email: "gianguyen130201@gmail.com",
  },
};

const level1 = {
  id: "ielts-01",
  title: "IELTS Level 01",
  subtitle: "Đầu vào 4.0 • Đầu ra 5.5+",
  intro:
    "Lớp học level 01 phù hợp với những bạn đã có nền tảng từ vựng và ngữ pháp cơ bản. Lớp học chuyên sâu, tập trung, không lan man, phù hợp với những bạn có mong muốn luyện thi IELTS.",
  basicInfo: [
    "Đầu ra 5.5+; đầu vào bắt buộc 4.0 hoặc hơn",
    "Hình thức: online qua Zoom",
    "Sĩ số: tối đa 10 người học",
    "Mỗi tuần 2 buổi, mỗi buổi 2+ giờ học",
    "Thời lượng: 30 buổi học - 60+ giờ học tổng cộng",
    "Vận dụng một phần mô hình blended learning với flipped classroom: ở nhà xem bài; lên lớp nghe giảng củng cố + luyện tập và được chỉnh sửa; sau lớp làm bài tập về nhà → phù hợp với bạn nào có thể dành tối thiểu 4 giờ tự học ở nhà",
  ],
  notes: [
    "Lớp học không nhận học thử",
    "Học phí hoàn thành trước ngày học",
  ],
  pricing: {
    schedule: "Lớp 01 tiếp theo dự kiến khai giảng vào tháng 5/2026.",
    duration: "30 buổi học chính thức (10 Nghe-Đọc, 10 Nói, 10 Viết) + 1 mock test Speaking & Writing miễn phí • Mỗi tuần 2 buổi • Mỗi buổi 2 giờ • Tổng cộng 60 giờ học • Lịch học theo giáo viên",
    tuition: "8.800.000 total 30 buổi (Không phát sinh)",
  },
  benefits: [
    "Mình, Gia Nguyễn (8.0 IELTS Overall - L8.5 | R9 | S8.5 | W8.0x4) trực tiếp đứng lớp, soạn tài liệu giảng dạy, chấm chữa bài và support các bạn.",
    "Feedback chi tiết cá nhân: mỗi bài nói/viết đều được nhận xét kỹ lưỡng, sửa lỗi và nâng cấp từ vựng – ngữ pháp – phát âm – kỹ thuật.",
    "Số lượng bài chữa Viết và Nói: 15 bài Viết (10 homework và 5 tự chọn), 8 homework Nói → Tất cả đều được feedback chi tiết, đến từng dấu chấm phẩy & bài viết: được viết lại gần như toàn bộ.",
    "Tài liệu học được biên soạn riêng, không lan man, bám sát format đề thi thật và phù hợp với trình độ, lồng ghép hoạt động bổ trợ.",
    "Hệ thống bài tập đầy đủ: gồm bài ôn trước – bài luyện trong buổi – bài tập về nhà sau buổi.",
    "Thư viện tài liệu bổ trợ: tài khoản tự học Reading/Listening + bài mẫu, từ vựng, templates IELTS Writing & Speaking.",
    "Hỗ trợ 1:1 ngoài giờ học: chữa bài, giải thích lỗi sai, định hướng học tập.",
    "Record bài giảng và lưu trữ đầy đủ, học viên có thể xem lại bất kỳ lúc nào.",
    "Lớp học độc quyền, không đại trà + Tuyển sinh có giới hạn (max 10) giúp mình kiểm soát năng lực và mặt bằng chung của lớp → điều chỉnh phương pháp, tài liệu, nội dung riêng biệt cho từng lớp để phù hợp với nhiều đối tượng nhất có thể.",
  ],
  curriculum: {
    listeningReading: [
      ["READING 1", "tổng quan bài đọc + completion"],
      ["READING 2", "multiple choice (trắc nghiệm)"],
      ["READING 3", "true false not given / yes no not given"],
      ["READING 4", "matching headings & matching features"],
      ["READING 5", "matching information & matching sentence endings"],
      ["LISTENING 1", "tổng quan bài nghe + completion (part 1 & 4)"],
      ["LISTENING 2", "matching"],
      ["LISTENING 3", "multiple choice"],
      ["LISTENING 4", "map"],
      ["LISTENING 5", "short answer question + q&a: listening & reading"],
    ],
    writing: [
      ["WRITING 1", "tổng quan writing + cách viết một đoạn văn có cấu trúc + opinion essay"],
      ["WRITING 2", "task 2: opinion essay cont. — nâng cấp đoạn văn"],
      ["WRITING 3", "task 1: process (quy trình)"],
      ["WRITING 4", "task 2: dạng bài discussion essay — discuss both views"],
      ["WRITING 5", "task 2: dạng bài lợi và hại (pros and cons)"],
      ["WRITING 6", "task 1: map (bản đồ)"],
      ["WRITING 7", "task 2: dạng bài C.E.S (cause effect solution)"],
      ["WRITING 8", "task 1: dynamic chart (biểu đồ động)"],
      ["WRITING 9", "task 2: dạng bài 2 câu hỏi (two-part questions)"],
      ["WRITING 10", "task 1: static chart (biểu đồ tĩnh)"],
    ],
    speaking: [
      ["SPEAKING 1", "describing people — part 1&2"],
      ["SPEAKING 2", "describing places — part 1&2"],
      ["SPEAKING 3", "describing work and study — part 1&2"],
      ["SPEAKING 4", "describing activites — part 1&2"],
      ["SPEAKING 5", "describing objects — part 1&2"],
      ["SPEAKING 6", "describing past events — part 1&2"],
      ["SPEAKING 7", "mock test 01 — lessons 123"],
      ["SPEAKING 8", "mock test 02 — lessons 456"],
      ["SPEAKING 9", "part 3: mở rộng ý tưởng tuyến tính — chủ đề urban life"],
      ["SPEAKING 10", "part 3: nguyên nhân, kết quả, giải pháp — chủ đề environment"],
    ],
  },
  faqs: [
    {
      q: "Lớp này mất gốc/ thấp hơn 4.0 có học được không?",
      a: [
        "Sorry nhưng mình e là sẽ khó và nặng cho bạn.",
        "Lớp học được thiết kế cho học viên có năng lực từ 4.0-4.5 IELTS (≈B1 CEFR) trở lên, không dành cho người dưới level này hoặc mất gốc. Hiện tại, mình chưa mở lớp Beginners; sau này có sẽ mong gặp và hỗ trợ được bạn.",
      ],
    },
    {
      q: "Lớp học 10 học viên thì làm sao thầy take care kĩ lưỡng được?",
      a: [
        "Không thành vấn đề.",
        "Lớp học của mình diễn ra trong 2 giờ hoặc hơn, sẽ là lúc 40-50% thời gian là giáo viên hướng dẫn lí thuyết. Vì thế, trên lớp, sẽ chỉ có ít hơn 40-50% là các bạn có thể thực hành và đặt câu hỏi. Tuy nhiên, những hỗ trợ sau giờ học (chấm chữa, giải đáp thắc mắc) hoàn toàn cá nhân hoá.",
        "Đối với Speaking: tất cả các bạn sẽ đều được luyện tập nói ở 40-50% thời lượng của buổi học & được mình chữa ngay trên lớp, thực chiến tại chỗ → chữa mẫu và điều chỉnh lỗi hệ thống để bạn có thể thực hành những câu khác và luyện tập theo nhóm. Bên cạnh đó, bạn được tặng kèm 3 giờ speaking coaching 1on1 cùng với mình; có thể chia đều 30 phút/session — hỗ trợ đến trước ngày thi thật.",
        "Đối với Writing: hầu hết các buổi học đầu tiên sẽ là thời gian mình nói lí thuyết + bạn sẽ cùng lên ý tưởng theo nhóm/cá nhân → mình chữa outline để bạn làm homework. Các buổi 5-6 về sau, các bạn sẽ được thực hành viết Body 1-2 theo ý tưởng trên lớp → mình chữa ngay trên lớp (1 hoặc một vài bạn).",
      ],
    },
    {
      q: "Có gì cần lưu ý ở lớp học không?",
      a: [
        "Có.",
        "Lớp học đơn giản, quy mô nhỏ. Tuy nhiên, để mọi thứ hiệu quả và suôn sẻ, các bạn được khuyến khích thực hiện (một phần) mô hình flipped classroom cùng với thầy giáo.",
        "Trước buổi học: xem bài trước ở nhà — mẫu bài học ở đây (từ vựng, ngữ pháp, cấu trúc bài, các câu hỏi cần thiết).",
        "Trong buổi học: giáo viên dùng công cụ minh hoạ bằng .pptx, hình ảnh, màu sắc, âm thanh, ứng dụng, công cụ trò chơi để minh hoạ bài giảng dạng thô—text → hỗ trợ hiểu bài + luyện tập & được chỉnh sửa + đặt câu hỏi.",
        "Sau buổi học: làm bài tập về nhà.",
      ],
    },
  ],
  placement: [
    "Đối với những bạn đã đi thi (đạt 4.0+) trước đây: chỉ cần báo điểm lần thi gần nhất cho mình.",
    "Với những bạn chưa từng thi: Bạn làm giúp mình test Ngữ pháp/ từ vựng, Nghe và Nói — yêu cầu: đạt B1.",
    "Nghe & Đọc: bạn làm qua EF SET Quick Check.",
    "Nói: mình trực tiếp test và định hướng cho bạn.",
    "Viết: Bạn sẽ viết 1 bài task 2 và gửi cho mình qua file .docx qua inbox.",
  ],
  writingPrompt:
    "The only reason why people work hard is to earn money and there is no other reason for doing so. To what extent do you agree or disagree?",
};

const level2 = {
  id: "ielts-02",
  title: "IELTS Level 02",
  subtitle: "Đầu vào 5.5–6.5 • Đầu ra +1 band",
  intro:
    "Lớp dành cho học viên đã có nền tảng B2, muốn học chuyên sâu hơn để nâng band điểm, đặc biệt ở Speaking và Writing, đồng thời vẫn có hệ thống ôn Listening & Reading rõ ràng.",
  basicInfo: [
    "Đầu vào: tối thiểu B2 cho cả 4 kỹ năng (5.5–6.5) → đầu ra: +1 band (6.5-7.5)",
    "Hình thức: online (qua Zoom)",
    "Sĩ số: tối đa 10 học viên",
    "Lịch học: 2 buổi/tuần — mỗi buổi 2-2.5 giờ",
    "Thời lượng: 34 buổi (~70+ giờ học)",
    "Vận hành một phần mô hình flipped classroom: trước buổi tự học trước; trong buổi học + củng cố + luyện + sửa; sau buổi làm homework + nhận feedback",
    "Phù hợp nếu bạn có thể dành ~4 giờ tự học/tuần",
  ],
  notes: ["Lớp học không nhận học thử", "Học phí hoàn tất trước ngày bắt đầu"],
  pricing: {
    schedule: "Lớp 02 tiếp theo dự kiến khai giảng vào 15/04/2026 • Lịch: tối 2-4 20:00-22:00",
    duration: "34 buổi (~70+ giờ học)",
    tuition: "Tổng cộng 10.000.000 (Không phát sinh)",
    speakingWriting: "Combo Speaking + Writing 9.000.000",
    oneOnOne: "600.000/buổi 2 giờ • Chỉ phù hợp với những bạn cần thi gấp hoặc không thể sắp xếp lịch học theo lớp nhóm",
  },
  benefits: [
    "Mình, Gia Nguyễn (8.0 IELTS Overall x 5 — L8.5 | R9 | S8.5 | W8.5) trực tiếp đứng lớp, soạn tài liệu, chấm chữa, và support.",
    "Feedback cá nhân hoá (Speaking & Writing) → sửa lỗi chi tiết + nâng cấp idea / vocab / grammar; rewrite bài viết dựa trên idea của bạn.",
    "11 homework Viết (trong khoá) + không giới hạn bài gửi thêm sau khoá.",
    "3 buổi speaking practice live cùng lớp (bắt buộc) + 3 giờ mock test 1-1 trong khoá + mock test 1-1 không giới hạn sau khoá đến ngày thi (≈30-45 phút/session).",
    "Tài liệu học được biên soạn riêng, không lan man, bám sát đề thi thật; gồm: bài xem trước (file pdf) + slide bài giảng + online quiz (nếu có) + file nghe + bài tập về nhà sau buổi.",
    "Thư viện tự học (Reading/Listening + samples + vocab) + hỗ trợ tài khoản luyện nghe/đọc 1-2 tháng trước khi thi.",
    "Record + tài liệu lưu trữ đầy đủ và lâu dài, học viên có thể xem lại bất kỳ lúc nào.",
    "Lớp học không đại trà, quy mô nhỏ → mình có thể điều chỉnh cách dạy và nội dung cho từng lớp.",
  ],
  curriculum: {
    writing: [
      ["WRITING 1", "Tổng quan task 2 (tiêu chí chấm điểm & cấu trúc bài) • Dạng bài opinion essay • Cách viết 40-60 • 'Hot word 01 🔥' — all • Chủ đề: transportation & urbanization"],
      ["WRITING 2", "Task Response • Big 'no-nos' trong Writing • 'Hot word 02 🔥' — the best/only way • Opinion essay cont. (with refutation) • Chủ đề: Crimes and punishments"],
      ["WRITING 3", "Nâng cấp ngữ pháp — complex and compound sentence • 'Hot word 03 🔥' — should • Chủ đề: Education"],
      ["WRITING 4", "Tổng quan writing task 1 • Dynamic charts"],
      ["WRITING 5", "Discussion essay • Referencing & Substitution • Linking without linkers — Thematic progression • Chủ đề: Art and Culture"],
      ["WRITING 6", "Task 1 - Static charts"],
      ["WRITING 7", "Nominalization, Collocations, Fixed phrases • Pros and cons • Chủ đề: Social media & Internet"],
      ["WRITING 8", "Task 1: Maps"],
      ["WRITING 9", "Hedging language • Task 2: C.E.S - Cause / Effect / Solution • Chủ đề: Environment"],
      ["WRITING 10", "Task 1: Process"],
      ["WRITING 11", "Two-part questions • Example-led paragraph • Chủ đề: Mixed"],
      ["WRITING 12", "Solving difficult questions • Chủ đề: Mixed"],
    ],
    speaking: [
      ["SPEAKING 1", "Tổng quan speaking • Part 1&2: mô tả người • Cấu trúc câu trả lời mạch lạc, súc tích"],
      ["SPEAKING 2", "Review bài 1 • Part 1&2: mô tả nơi chốn • Pronunciation: Chunking & rhythm • Cấu trúc câu trả lời cont."],
      ["SPEAKING 3", "Part 3 — Relationships / Cities / Countryside • 2 techniques: Linear expansion + Concession"],
      ["REVISION 01", "Revision 01 — Lessons 123"],
      ["SPEAKING 4", "Part 1&2: mô tả công việc • Các diễn đạt công việc & bận rộn • 'Recyclability mindset' — learn less, use more"],
      ["SPEAKING 5", "Review bài 4 • Part 1&2: mô tả hoạt động • sở thích & well-being benefits • relative clause • Sentence stress & Intonation"],
      ["SPEAKING 6", "Part 3 — Stress, Time and Hobbies • Comparing: Past-Present / Different bases / Pros-cons"],
      ["REVISION 02", "Revision 02 — Lessons 456"],
      ["SPEAKING 9", "Part 1&2: mô tả đồ vật • Present perfect / Present continuous / Present simple • Linking"],
      ["SPEAKING 10", "Review bài 9 • Part 1&2: mô tả sự kiện • Storytelling • Past tenses • -ed, Assimilation"],
      ["SPEAKING 11", "Part 3 — Environment, History • Cause-Effect-Sollution + 'I don't know'"],
      ["SPEAKING 12", "Revision 03 — Lessons 9-11 • Consolidation"],
    ],
    listeningReading: [
      ["READING 1", "Overview + Matching headings"],
      ["READING 2", "Multiple choice"],
      ["READING 3", "True false not given / yes no not given"],
      ["READING 4", "Matchings: features - information - sentence endings"],
      ["READING 5", "Note / table / diagram / summary completion + Q&A"],
      ["LISTENING 1", "Overview + Form completion (Listening part 1)"],
      ["LISTENING 2", "Multiple choice + Map (Listening part 2)"],
      ["LISTENING 3", "Matching (Listening part 3)"],
      ["LISTENING 4", "Multiple choice (Listening part 3)"],
      ["LISTENING 5", "Note / table / diagram completion + short answer question (Listening part 4) + Q&A"],
    ],
  },
  faqs: [
    {
      q: "Mình có thể aim 7.0-7.5 không?",
      a: [
        "Được.",
        "Lớp học đầu ra 6.5++ → có thể hỗ trợ bạn đạt aim 7.0+, và thực tế, đã có nhiều bạn đạt 7.5 và 8.0 Overall sau khoá học.",
        "Tài nguyên giảng dạy được thiết kế chuẩn hoá đến ngưỡng 8.0+ → tuỳ vào khả năng khai thác ở người học.",
        "Bài chấm chữa Speaking / Writing là cá nhân hoá, được chỉnh sửa từ triển khai ý tưởng, ngữ pháp, từ vựng, cho tới từng dấu chấm phẩy; được viết lại dựa trên ý tưởng của bạn bởi các nâng cấp về diễn đạt.",
      ],
    },
    {
      q: "Lớp học 10 học viên thì làm sao thầy take care kĩ lưỡng được?",
      a: [
        "Why not?",
        "Lớp học của mình diễn ra trong 2 giờ hoặc hơn, sẽ là lúc 40-50% thời gian là giáo viên hướng dẫn lí thuyết. Vì thế, trên lớp, sẽ chỉ có ít hơn 40-50% là các bạn có thể thực hành và đặt câu hỏi. Tuy nhiên, những hỗ trợ sau giờ học (chấm chữa, giải đáp thắc mắc) hoàn toàn cá nhân hoá.",
        "Đối với Speaking: tất cả các bạn sẽ đều được luyện tập nói ở 40-50% thời lượng của buổi học & được mình chữa ngay trên lớp. Bên cạnh đó, bạn được tặng kèm 3 giờ speaking coaching 1on1 cùng với mình.",
        "Đối với Writing: các buổi đầu thiên về lí thuyết + lên ý tưởng; những buổi sau sẽ viết và được chữa ngay trên lớp.",
      ],
    },
    {
      q: "Có gì cần lưu ý ở lớp học không?",
      a: [
        "Có.",
        "Trước buổi học: xem bài trước ở nhà.",
        "Trong buổi học: giáo viên dùng .pptx, hình ảnh, màu sắc, âm thanh, ứng dụng, công cụ trò chơi để minh hoạ bài giảng và hỗ trợ luyện tập.",
        "Sau buổi học: làm bài tập về nhà.",
      ],
    },
    {
      q: "Có đảm bảo đầu ra không?",
      a: ["Không."],
    },
  ],
  placement: [
    "Với những bạn đã từng thi trước đây và đạt điểm 5.5+: chỉ cần cung cấp điểm thi gần nhất.",
    "Với những bạn chưa từng thi: làm test Ngữ pháp/ từ vựng, Nghe và Nói — yêu cầu: đạt B2.",
    "Nghe & Đọc: làm qua EF SET Quick Check.",
    "Nói: record một đoạn giới thiệu bản thân 1 phút gửi cho mình.",
    "Viết: viết 1 bài task 2 và gửi qua file .docx qua inbox.",
  ],
  writingPrompt:
    "The only reason why people work hard is to earn money and there is no other reason for doing so. To what extent do you agree or disagree?",
};

const writingService = {
  title: "Dịch vụ chấm chữa IELTS Writing",
  intro:
    "Các bài viết không những được chấm chữa chi tiết theo 4 tiêu chí mà còn gần như được viết lại toàn bộ với những nâng cấp về diễn đạt band 8+ (cho bạn nào aim 7+W) và band 7+ (cho bạn nào aim 6+ Writing).",
  packages: [
    {
      name: "LẺ 1 BÀI",
      detail: "Đề: bạn chọn • Trả bài sau 5 ngày • HSD: 1 năm",
      price: "150.000/bài",
    },
    {
      name: "GÓI 5 BÀI",
      detail: "Đề: bạn chọn • Gửi qua 1 folder Google Drive • Gửi đến đâu chấm đến đó • Trả bài sau 5 ngày • HSD: 1 năm",
      price: "625.000/5 bài",
    },
    {
      name: "GÓI 10 BÀI",
      detail: "Tương tự gói 5 bài (nhưng là 10 bài)",
      price: "1.000.000/10 bài",
    },
    {
      name: "GÓI INPUT TASK 2 + CHẤM CHỮA 10 BÀI",
      detail:
        "Đề mình chọn - chỉ task 2 • Có bài báo/học liệu liên quan để đọc, tóm tắt rồi viết • Mình sửa cả bài tóm tắt và bài viết • Có sample mình đạt điểm thật do IDP/cựu giám khảo chấm • HSD: trong vòng 1 năm • Nếu bạn thi gấp trong 2 tháng, mình sẽ ưu tiên chấm liên tục trong 1 tháng đủ bài • Nếu thi đạt, mình sẽ refund 5% phí chấm chữa như một món quà",
      price: "1.500.000/10 bài task 2",
      bestseller: true,
    },
  ],
};

const bizClass = {
  title: "Tiếng Anh giao tiếp công sở (biz)",
  status: "Lớp hiện đóng tuyển sinh. Sẽ thông báo khi có lịch tuyển sinh mới.",
  overview: [
    "Mục tiêu: vận dụng những gì đã học để giao tiếp ở nơi làm việc.",
    "Hình thức: Offline.",
    "Sĩ số: tối đa 8 người học.",
    "Mỗi tuần 2 buổi, mỗi buổi 1.5+ giờ học.",
    "Thời lượng: 18 buổi học (level 1) và 30 buổi học (level 2 đến 5).",
    "Phù hợp với người đi làm, cần tiếng Anh và làm việc trong môi trường phải sử dụng tiếng Anh; hoặc người đi làm có nhu cầu bổ sung ngoại ngữ để tìm kiếm thêm cơ hội/công việc khác có mức thu nhập tốt hơn.",
  ],
};

function openNewTab(url) {
  window.open(url, "_blank", "noopener,noreferrer");
}

function GradientBlob({ className = "" }) {
  return (
    <div
      className={`absolute rounded-full blur-3xl opacity-40 pointer-events-none ${className}`}
      style={{
        background:
          "radial-gradient(circle at 30% 30%, rgba(59,130,246,0.22), rgba(148,163,184,0.2), rgba(14,165,233,0.16))",
      }}
    />
  );
}

function SectionTitle({ eyebrow, title, desc }) {
  return (
    <div className="space-y-3">
      {eyebrow && <div className="text-sm font-medium text-slate-500">{eyebrow}</div>}
      <h2 className="text-2xl md:text-4xl font-semibold tracking-tight text-slate-900">{title}</h2>
      {desc && <p className="text-slate-600 max-w-3xl leading-7">{desc}</p>}
    </div>
  );
}

function Stat({ icon: Icon, label, value }) {
  return (
    <div className="rounded-2xl border border-slate-200/70 bg-gradient-to-br from-white/95 to-slate-100/90 backdrop-blur p-4 shadow-sm">
      <div className="flex items-center gap-3 text-slate-500 mb-2">
        <Icon className="w-4 h-4" />
        <span className="text-sm">{label}</span>
      </div>
      <div className="text-lg font-semibold text-slate-900">{value}</div>
    </div>
  );
}

function Pill({ children }) {
  return (
    <span className="inline-flex items-center rounded-full border border-slate-200/80 bg-slate-50/90 px-3 py-1 text-sm text-slate-700 shadow-sm">
      {children}
    </span>
  );
}

function LinkButton({ children, onClick }) {
  return (
    <Button onClick={onClick} variant="outline" className="rounded-full bg-white/80 hover:bg-white">
      {children}
      <ExternalLink className="w-4 h-4 ml-2" />
    </Button>
  );
}

function CurriculumTable({ title, items }) {
  return (
    <Card className="rounded-3xl border-slate-200/80 shadow-sm bg-white/80 backdrop-blur">
      <CardHeader>
        <CardTitle className="text-xl text-slate-900">{title}</CardTitle>
      </CardHeader>
      <CardContent>
        <div className="space-y-3">
          {items.map(([name, detail], idx) => (
            <motion.div
              key={name}
              initial={{ opacity: 0, y: 12 }}
              whileInView={{ opacity: 1, y: 0 }}
              viewport={{ once: true }}
              transition={{ duration: 0.35, delay: idx * 0.02 }}
              className="grid md:grid-cols-[180px_1fr] gap-3 rounded-2xl border border-slate-100 p-4 bg-gradient-to-br from-white to-slate-50 hover:border-slate-200 hover:shadow-sm transition-all"
            >
              <div className="font-semibold text-slate-900">{name}</div>
              <div className="text-slate-600 leading-7">{detail}</div>
            </motion.div>
          ))}
        </div>
      </CardContent>
    </Card>
  );
}

function FAQItem({ q, a }) {
  const [open, setOpen] = useState(false);
  return (
    <div className="rounded-2xl border border-slate-200 bg-white overflow-hidden">
      <button
        onClick={() => setOpen(!open)}
        className="w-full flex items-center justify-between gap-4 p-5 text-left"
      >
        <span className="font-medium text-slate-900">{q}</span>
        <ChevronDown className={`w-5 h-5 text-slate-500 transition-transform ${open ? "rotate-180" : ""}`} />
      </button>
      <AnimatePresence initial={false}>
        {open && (
          <motion.div
            initial={{ height: 0, opacity: 0 }}
            animate={{ height: "auto", opacity: 1 }}
            exit={{ height: 0, opacity: 0 }}
            transition={{ duration: 0.28 }}
          >
            <div className="px-5 pb-5 space-y-3 text-slate-600 leading-7">
              {a.map((item, i) => (
                <p key={i}>{item}</p>
              ))}
            </div>
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  );
}

function Hero({ go }) {
  return (
    <section className="relative overflow-hidden px-4 md:px-8 pt-8 md:pt-12">
      <div className="max-w-7xl mx-auto relative">
        <GradientBlob className="w-72 h-72 -top-16 -left-10" />
        <GradientBlob className="w-96 h-96 top-10 right-0" />
        <div className="relative rounded-[2rem] border border-slate-200/70 bg-gradient-to-br from-slate-50/95 via-sky-50/85 to-blue-50/80 backdrop-blur-xl shadow-xl p-6 md:p-10">
          <div className="grid lg:grid-cols-[1.2fr_0.8fr] gap-8 items-center">
            <div className="space-y-6">
              <Badge className="rounded-full bg-slate-800 hover:bg-slate-800 text-white px-4 py-1.5">The Language Town • Course Booklet</Badge>
              <div className="space-y-4">
                <h1 className="text-4xl md:text-6xl font-semibold tracking-tight text-slate-900 leading-tight">
                  Lớp học của Nguyễn
                </h1>
                <p className="text-lg md:text-xl text-slate-600 max-w-2xl leading-8">
                  Khám phá các lớp học IELTS và dịch vụ học thuật với lộ trình rõ ràng, mô hình lớp nhỏ, và hỗ trợ cá nhân hoá.
                </p>
              </div>
              <div className="flex flex-wrap gap-3">
                <Button onClick={() => go("ielts-01")} className="rounded-full px-6 py-6 text-base bg-slate-800 hover:bg-slate-700 text-white shadow-md">
                  Xem lớp IELTS 01
                  <ArrowRight className="w-4 h-4 ml-2" />
                </Button>
                <Button variant="outline" onClick={() => go("ielts-02")} className="rounded-full px-6 py-6 text-base bg-slate-100 border-slate-200 text-slate-800 hover:bg-slate-200">
                  Xem lớp IELTS 02
                </Button>
              </div>
              <div className="flex flex-wrap gap-2 pt-2">
                <Pill>Minimal</Pill>
                <Pill>Clean</Pill>
                <Pill>Interactive</Pill>
                <Pill>Smooth animation</Pill>
              </div>
            </div>
            <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <Stat icon={Users} label="Quy mô lớp" value="Tối đa 10 học viên" />
              <Stat icon={Monitor} label="Hình thức" value="Online qua Zoom" />
              <Stat icon={Clock3} label="Mô hình" value="Blended + flipped classroom" />
              <Stat icon={GraduationCap} label="Teacher" value="8.0 IELTS Overall x5" />
            </div>
          </div>
        </div>
      </div>
    </section>
  );
}

function TeacherCard() {
  return (
    <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/60 backdrop-blur shadow-sm">
      <CardContent className="p-6 md:p-8">
        <div className="flex flex-col lg:flex-row gap-8 lg:items-start">
          <div className="flex-1 space-y-4">
            <Badge className="rounded-full bg-sky-100 text-slate-700 hover:bg-sky-100">Teacher profile</Badge>
            <h3 className="text-2xl md:text-3xl font-semibold text-slate-900">{teacher.name}</h3>
            <p className="text-slate-600 leading-7">{teacher.shortBio}</p>
            <div className="space-y-3">
              {teacher.achievements.map((item) => (
                <div key={item} className="flex gap-3">
                  <CheckCircle2 className="w-5 h-5 mt-1 text-emerald-500 shrink-0" />
                  <p className="text-slate-700 leading-7">{item}</p>
                </div>
              ))}
            </div>
          </div>
          <div className="lg:w-[320px] space-y-4">
            <div className="rounded-3xl bg-gradient-to-br from-slate-800 via-slate-700 to-sky-800 text-white p-6 shadow-lg">
              <div className="text-sm text-slate-300 mb-2">Headline</div>
              <div className="text-xl font-semibold leading-8">{teacher.headline}</div>
            </div>
            <div className="rounded-3xl border border-slate-200 p-5 bg-white">
              <div className="space-y-3 text-slate-700">
                <div className="flex items-center gap-3"><Phone className="w-4 h-4" /> {teacher.contact.phone}</div>
                <div className="flex items-center gap-3 break-all"><Mail className="w-4 h-4" /> {teacher.contact.email}</div>
              </div>
              <div className="flex flex-wrap gap-2 mt-5">
                <LinkButton onClick={() => openNewTab(links.teacherProof)}>Bằng cấp</LinkButton>
                <LinkButton onClick={() => openNewTab(links.teacherFeedback)}>Feedback</LinkButton>
              </div>
            </div>
          </div>
        </div>
      </CardContent>
    </Card>
  );
}

function HomePage({ go }) {
  return (
    <div className="space-y-10 md:space-y-16 pb-16">
      <Hero go={go} />

      <section className="px-4 md:px-8">
        <div className="max-w-7xl mx-auto">
          <SectionTitle
            eyebrow="Menu lớp học"
            title="Chọn đúng lộ trình phù hợp với bạn"
            desc="Mỗi mục được trình bày như một trải nghiệm website riêng. Khi bấm vào từng lớp, bạn sẽ đi tới trang chi tiết có lộ trình, quyền lợi, FAQ, tài liệu mẫu và kiểm tra đầu vào."
          />
          <div className="grid lg:grid-cols-2 xl:grid-cols-4 gap-5 mt-8">
            {[
              {
                title: "IELTS Level 01",
                subtitle: "Đầu vào 4.0 • Đầu ra 5.5+",
                icon: BookOpen,
                action: () => go("ielts-01"),
              },
              {
                title: "IELTS Level 02",
                subtitle: "Đầu vào 5.5–6.5 • Đầu ra +1 band",
                icon: GraduationCap,
                action: () => go("ielts-02"),
              },
              {
                title: "Chấm chữa IELTS Writing",
                subtitle: "Các gói sửa bài chi tiết",
                icon: FileText,
                action: () => go("writing-service"),
              },
              {
                title: "English for Work (Biz)",
                subtitle: "Hiện đóng tuyển sinh",
                icon: BriefcaseBusiness,
                action: () => go("biz"),
              },
            ].map((item, idx) => {
              const Icon = item.icon;
              return (
                <motion.div
                  key={item.title}
                  initial={{ opacity: 0, y: 16 }}
                  whileInView={{ opacity: 1, y: 0 }}
                  viewport={{ once: true }}
                  transition={{ duration: 0.35, delay: idx * 0.06 }}
                >
                  <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-blue-50/60 backdrop-blur hover:shadow-lg hover:-translate-y-1 transition-all group h-full">
                    <CardContent className="p-6 flex flex-col h-full">
                      <div className="w-12 h-12 rounded-2xl bg-gradient-to-br from-slate-100 via-sky-100 to-blue-100 flex items-center justify-center mb-5 group-hover:scale-105 transition-transform">
                        <Icon className="w-6 h-6 text-slate-800" />
                      </div>
                      <h3 className="text-xl font-semibold text-slate-900 mb-2">{item.title}</h3>
                      <p className="text-slate-600 leading-7 flex-1">{item.subtitle}</p>
                      <Button onClick={item.action} variant="ghost" className="justify-start px-0 mt-5 text-slate-900">
                        Xem chi tiết <ArrowRight className="w-4 h-4 ml-2" />
                      </Button>
                    </CardContent>
                  </Card>
                </motion.div>
              );
            })}
          </div>
        </div>
      </section>

      <section className="px-4 md:px-8">
        <div className="max-w-7xl mx-auto">
          <TeacherCard />
        </div>
      </section>

      <section className="px-4 md:px-8">
        <div className="max-w-7xl mx-auto grid lg:grid-cols-[1.05fr_0.95fr] gap-6">
          <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
            <CardContent className="p-6 md:p-8 space-y-5">
              <SectionTitle
                eyebrow="Điểm nổi bật"
                title="Mô hình lớp nhỏ, nội dung tập trung"
                desc="Website này giữ nguyên tinh thần booklet: học chuyên sâu, không lan man, nhiều hỗ trợ cá nhân hoá và có hệ thống học trước – học trong buổi – homework sau buổi."
              />
              <div className="grid sm:grid-cols-2 gap-3">
                {[
                  "Feedback cá nhân hoá",
                  "Record lưu trữ đầy đủ",
                  "Tài liệu biên soạn riêng",
                  "Lộ trình rõ ràng theo kỹ năng",
                  "Mock test đi kèm",
                  "Hỗ trợ ngoài giờ học",
                ].map((item) => (
                  <div key={item} className="rounded-2xl bg-gradient-to-br from-slate-50 to-sky-50/70 border border-slate-100 px-4 py-3 text-slate-700">
                    {item}
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>

          <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-slate-800 via-slate-700 to-sky-800 text-white overflow-hidden">
            <CardContent className="p-6 md:p-8 relative">
              <GradientBlob className="w-72 h-72 -right-8 -bottom-8 opacity-60" />
              <div className="relative space-y-5">
                <Badge className="rounded-full bg-white/10 text-white hover:bg-white/10">Liên hệ nhanh</Badge>
                <h3 className="text-2xl font-semibold">Kết nối với Nguyễn</h3>
                <div className="space-y-3 text-slate-200">
                  <div className="flex gap-3"><Phone className="w-4 h-4 mt-1" /> <span>{teacher.contact.phone}</span></div>
                  <div className="flex gap-3 break-all"><Mail className="w-4 h-4 mt-1" /> <span>{teacher.contact.email}</span></div>
                </div>
                <div className="flex flex-wrap gap-2 pt-2">
                  <Button onClick={() => openNewTab(links.facebook)} variant="secondary" className="rounded-full"><Globe className="w-4 h-4 mr-2" />Facebook</Button>
                  <Button onClick={() => openNewTab(links.threads)} variant="secondary" className="rounded-full"><MessageCircle className="w-4 h-4 mr-2" />Threads</Button>
                  <Button onClick={() => openNewTab(links.instagram)} variant="secondary" className="rounded-full"><Globe className="w-4 h-4 mr-2" />Instagram</Button>
                </div>
              </div>
            </CardContent>
          </Card>
        </div>
      </section>
    </div>
  );
}

function CourseHero({ course, accent = "indigo", onBack }) {
  const accents = {
    indigo: "from-slate-200/70 via-sky-100/60 to-blue-100/50",
    emerald: "from-slate-200/70 via-sky-100/60 to-cyan-100/50",
  };
  return (
    <div className="relative overflow-hidden rounded-[2rem] border border-slate-200/70 bg-gradient-to-br from-white via-slate-50 to-sky-50/70 backdrop-blur-xl shadow-lg p-6 md:p-8">
      <div className={`absolute inset-0 bg-gradient-to-br ${accents[accent]}`} />
      <div className="relative space-y-5">
        <Button variant="ghost" onClick={onBack} className="rounded-full -ml-3 text-slate-700">
          <Home className="w-4 h-4 mr-2" /> Về trang chính
        </Button>
        <Badge className="rounded-full bg-slate-100/90 text-slate-900 hover:bg-slate-100/90">Chi tiết lớp học</Badge>
        <div className="space-y-3">
          <h1 className="text-3xl md:text-5xl font-semibold tracking-tight text-slate-900">{course.title}</h1>
          <p className="text-lg text-slate-600">{course.subtitle}</p>
          <p className="text-slate-700 max-w-3xl leading-8">{course.intro}</p>
        </div>
      </div>
    </div>
  );
}

function CoursePage({ course, onBack, extraLinks, accent = "indigo" }) {
  return (
    <div className="px-4 md:px-8 py-8 md:py-10">
      <div className="max-w-7xl mx-auto space-y-8">
        <CourseHero course={course} onBack={onBack} accent={accent} />

        <div className="grid lg:grid-cols-[0.9fr_1.1fr] gap-6">
          <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
            <CardHeader>
              <CardTitle className="text-2xl">Thông tin cơ bản</CardTitle>
            </CardHeader>
            <CardContent className="space-y-4">
              {course.basicInfo.map((item) => (
                <div key={item} className="flex gap-3">
                  <Sparkles className="w-4 h-4 mt-1 text-slate-500 shrink-0" />
                  <p className="text-slate-700 leading-7">{item}</p>
                </div>
              ))}
              <Separator />
              <div className="space-y-2">
                {course.notes.map((note) => (
                  <Badge key={note} variant="outline" className="mr-2 mb-2 rounded-full py-1.5 px-3">{note}</Badge>
                ))}
              </div>
            </CardContent>
          </Card>

          <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-slate-800 via-slate-700 to-sky-800 text-white overflow-hidden">
            <CardContent className="p-6 md:p-8 relative">
              <GradientBlob className="w-80 h-80 -right-10 -top-10 opacity-60" />
              <div className="relative space-y-5">
                <h3 className="text-2xl font-semibold">Thời lượng & học phí</h3>
                <div className="grid sm:grid-cols-2 gap-4">
                  <div className="rounded-2xl bg-white/10 p-4">
                    <div className="text-sm text-slate-300 mb-2">Lịch học</div>
                    <div className="leading-7">{course.pricing.schedule}</div>
                  </div>
                  <div className="rounded-2xl bg-white/10 p-4">
                    <div className="text-sm text-slate-300 mb-2">Thời lượng</div>
                    <div className="leading-7">{course.pricing.duration}</div>
                  </div>
                  <div className="rounded-2xl bg-white/10 p-4 sm:col-span-2">
                    <div className="text-sm text-slate-300 mb-2">Học phí</div>
                    <div className="text-xl font-semibold">{course.pricing.tuition}</div>
                    {course.pricing.speakingWriting && <div className="mt-2 text-slate-200">{course.pricing.speakingWriting}</div>}
                    {course.pricing.oneOnOne && <div className="mt-2 text-slate-300">{course.pricing.oneOnOne}</div>}
                  </div>
                </div>
              </div>
            </CardContent>
          </Card>
        </div>

        <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
          <CardHeader>
            <CardTitle className="text-2xl">Quyền lợi</CardTitle>
          </CardHeader>
          <CardContent>
            <div className="grid md:grid-cols-2 gap-4">
              {course.benefits.map((item, idx) => (
                <motion.div
                  key={item}
                  initial={{ opacity: 0, y: 12 }}
                  whileInView={{ opacity: 1, y: 0 }}
                  viewport={{ once: true }}
                  transition={{ duration: 0.3, delay: idx * 0.02 }}
                  className="rounded-2xl border border-slate-100 p-4 bg-gradient-to-br from-slate-50 to-sky-50/60"
                >
                  <div className="flex gap-3">
                    <CheckCircle2 className="w-5 h-5 mt-1 text-emerald-500 shrink-0" />
                    <p className="text-slate-700 leading-7">{item}</p>
                  </div>
                </motion.div>
              ))}
            </div>
          </CardContent>
        </Card>

        <div className="grid xl:grid-cols-3 gap-6">
          {course.curriculum.listeningReading && (
            <CurriculumTable title="Listening & Reading" items={course.curriculum.listeningReading} />
          )}
          {course.curriculum.writing && <CurriculumTable title="Writing" items={course.curriculum.writing} />}
          {course.curriculum.speaking && <CurriculumTable title="Speaking" items={course.curriculum.speaking} />}
        </div>

        <div className="grid lg:grid-cols-[1fr_1fr] gap-6">
          <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
            <CardHeader>
              <CardTitle className="text-2xl">Kiểm tra đầu vào</CardTitle>
            </CardHeader>
            <CardContent className="space-y-4">
              {course.placement.map((item) => (
                <div key={item} className="flex gap-3">
                  <ArrowRight className="w-4 h-4 mt-1 text-slate-500 shrink-0" />
                  <p className="text-slate-700 leading-7">{item}</p>
                </div>
              ))}
              <div className="rounded-2xl bg-slate-900 text-white p-5 mt-5">
                <div className="text-sm text-slate-300 mb-2">Writing placement prompt</div>
                <p className="leading-7">{course.writingPrompt}</p>
              </div>
              <div className="flex flex-wrap gap-3 pt-2">
                <LinkButton onClick={() => openNewTab(links.efset)}>EF SET Quick Check</LinkButton>
              </div>
            </CardContent>
          </Card>

          <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
            <CardHeader>
              <CardTitle className="text-2xl">FAQs</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              {course.faqs.map((item) => (
                <FAQItem key={item.q} q={item.q} a={item.a} />
              ))}
            </CardContent>
          </Card>
        </div>

        <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
          <CardHeader>
            <CardTitle className="text-2xl">Tài liệu mẫu & links mở tab mới</CardTitle>
          </CardHeader>
          <CardContent className="flex flex-wrap gap-3">
            {extraLinks.map((item) => (
              <LinkButton key={item.label} onClick={() => openNewTab(item.href)}>{item.label}</LinkButton>
            ))}
          </CardContent>
        </Card>
      </div>
    </div>
  );
}

function WritingServicePage({ onBack }) {
  return (
    <div className="px-4 md:px-8 py-8 md:py-10">
      <div className="max-w-7xl mx-auto space-y-8">
        <div className="rounded-[2rem] border border-white/60 bg-white/75 backdrop-blur-xl shadow-lg p-6 md:p-8">
          <Button variant="ghost" onClick={onBack} className="rounded-full -ml-3 text-slate-700">
            <Home className="w-4 h-4 mr-2" /> Về trang chính
          </Button>
          <div className="space-y-4 mt-3">
            <Badge className="rounded-full bg-slate-100/90 text-slate-900 hover:bg-slate-100/90">Writing service</Badge>
            <h1 className="text-3xl md:text-5xl font-semibold tracking-tight text-slate-900">{writingService.title}</h1>
            <p className="text-slate-700 max-w-4xl leading-8">{writingService.intro}</p>
          </div>
        </div>

        <div className="grid md:grid-cols-2 gap-5">
          {writingService.packages.map((pkg, idx) => (
            <motion.div key={pkg.name} initial={{ opacity: 0, y: 16 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.35, delay: idx * 0.05 }}>
              <Card className={`rounded-[2rem] h-full border-slate-200/80 ${pkg.bestseller ? "bg-gradient-to-br from-slate-800 via-slate-700 to-sky-800 text-white" : "bg-gradient-to-br from-white via-slate-50 to-sky-50/50"}`}>
                <CardContent className="p-6 md:p-7 space-y-4 h-full flex flex-col">
                  <div className="flex items-center justify-between gap-4">
                    <h3 className="text-xl font-semibold">{pkg.name}</h3>
                    {pkg.bestseller && <Badge className="rounded-full bg-white text-slate-900 hover:bg-white">Best-seller</Badge>}
                  </div>
                  <p className={`${pkg.bestseller ? "text-slate-200" : "text-slate-600"} leading-7 flex-1`}>{pkg.detail}</p>
                  <div className={`text-2xl font-semibold ${pkg.bestseller ? "text-white" : "text-slate-900"}`}>{pkg.price}</div>
                </CardContent>
              </Card>
            </motion.div>
          ))}
        </div>

        <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
          <CardHeader>
            <CardTitle className="text-2xl">Mở tài liệu mẫu ở tab mới</CardTitle>
          </CardHeader>
          <CardContent className="flex flex-wrap gap-3">
            <LinkButton onClick={() => openNewTab(links.level2WritingSamples)}>Xem mẫu chấm chữa</LinkButton>
            <LinkButton onClick={() => openNewTab(links.teacherFeedback)}>Feedback học viên</LinkButton>
          </CardContent>
        </Card>
      </div>
    </div>
  );
}

function BizPage({ onBack }) {
  return (
    <div className="px-4 md:px-8 py-8 md:py-10">
      <div className="max-w-7xl mx-auto space-y-8">
        <div className="rounded-[2rem] border border-white/60 bg-white/75 backdrop-blur-xl shadow-lg p-6 md:p-8">
          <Button variant="ghost" onClick={onBack} className="rounded-full -ml-3 text-slate-700">
            <Home className="w-4 h-4 mr-2" /> Về trang chính
          </Button>
          <div className="space-y-4 mt-3">
            <Badge className="rounded-full bg-slate-200 text-slate-700 hover:bg-slate-200">Hiện đóng tuyển sinh</Badge>
            <h1 className="text-3xl md:text-5xl font-semibold tracking-tight text-slate-900">{bizClass.title}</h1>
            <p className="text-slate-700 max-w-4xl leading-8">{bizClass.status}</p>
          </div>
        </div>

        <Card className="rounded-[2rem] border-slate-200/80 bg-gradient-to-br from-white via-slate-50 to-sky-50/50">
          <CardHeader>
            <CardTitle className="text-2xl">Tổng quan</CardTitle>
          </CardHeader>
          <CardContent className="space-y-4">
            {bizClass.overview.map((item) => (
              <div key={item} className="flex gap-3">
                <CheckCircle2 className="w-5 h-5 mt-1 text-emerald-500 shrink-0" />
                <p className="text-slate-700 leading-7">{item}</p>
              </div>
            ))}
          </CardContent>
        </Card>
      </div>
    </div>
  );
}

export default function InteractiveCourseBookletWebsite() {
  const [page, setPage] = useState("home");

  const navbarItems = useMemo(
    () => [
      { key: "home", label: "Trang chính" },
      { key: "ielts-01", label: "IELTS 01" },
      { key: "ielts-02", label: "IELTS 02" },
      { key: "writing-service", label: "Writing" },
    ],
    []
  );

  return (
    <div className="min-h-screen bg-[radial-gradient(circle_at_top,_rgba(248,250,252,1),_rgba(241,245,249,1),_rgba(226,232,240,0.95))] text-slate-900">
      <header className="sticky top-0 z-40 border-b border-slate-200/70 bg-white/80 backdrop-blur-xl">
        <div className="max-w-7xl mx-auto px-4 md:px-8 h-16 flex items-center justify-between gap-4">
          <button onClick={() => setPage("home")} className="font-semibold tracking-tight text-slate-900">
            The Language Town
          </button>
          <nav className="hidden md:flex items-center gap-2">
            {navbarItems.map((item) => (
              <button
                key={item.key}
                onClick={() => setPage(item.key)}
                className={`px-4 py-2 rounded-full text-sm transition-all ${page === item.key ? "bg-slate-800 text-white" : "text-slate-600 hover:bg-slate-100"}`}
              >
                {item.label}
              </button>
            ))}
          </nav>
          <Button onClick={() => openNewTab(links.fanpage)} className="rounded-full hidden sm:inline-flex bg-slate-800 hover:bg-slate-700 text-white">
            Fanpage
            <ExternalLink className="w-4 h-4 ml-2" />
          </Button>
        </div>
      </header>

      <AnimatePresence mode="wait">
        <motion.main
          key={page}
          initial={{ opacity: 0, y: 14 }}
          animate={{ opacity: 1, y: 0 }}
          exit={{ opacity: 0, y: -10 }}
          transition={{ duration: 0.28 }}
        >
          {page === "home" && <HomePage go={setPage} />}
          {page === "ielts-01" && (
            <CoursePage
              course={level1}
              accent="indigo"
              onBack={() => setPage("home")}
              extraLinks={[
                { label: "Record lớp Level 1", href: links.level1Record },
                { label: "Mẫu bài học", href: links.level1LessonSamples },
                { label: "Mẫu chấm chữa Writing", href: links.level1WritingSamples },
                { label: "Bằng cấp", href: links.teacherProof },
                { label: "Feedback học viên", href: links.teacherFeedback },
              ]}
            />
          )}
          {page === "ielts-02" && (
            <CoursePage
              course={level2}
              accent="emerald"
              onBack={() => setPage("home")}
              extraLinks={[
                { label: "Record lớp Level 2", href: links.level2Record },
                { label: "Mẫu tài liệu", href: links.level2LessonSamples },
                { label: "Mẫu chấm chữa Writing", href: links.level2WritingSamples },
                { label: "Bằng cấp", href: links.teacherProof },
                { label: "Feedback học viên", href: links.teacherFeedback },
              ]}
            />
          )}
          {page === "writing-service" && <WritingServicePage onBack={() => setPage("home")} />}
          {page === "biz" && <BizPage onBack={() => setPage("home")} />}
        </motion.main>
      </AnimatePresence>

      <footer className="px-4 md:px-8 py-10 border-t border-slate-200/70 bg-white/70 backdrop-blur-xl">
        <div className="max-w-7xl mx-auto flex flex-col md:flex-row gap-4 items-start md:items-center justify-between">
          <div>
            <div className="font-semibold text-slate-900">Lớp học của Nguyễn</div>
            <div className="text-slate-600 mt-1">Interactive booklet website • minimal • clean • modern</div>
          </div>
          <div className="flex flex-wrap gap-2">
            <Button variant="outline" className="rounded-full" onClick={() => openNewTab(links.facebook)}><Globe className="w-4 h-4 mr-2" />Facebook</Button>
            <Button variant="outline" className="rounded-full" onClick={() => openNewTab(links.threads)}>Threads</Button>
            <Button variant="outline" className="rounded-full" onClick={() => openNewTab(links.instagram)}><Globe className="w-4 h-4 mr-2" />Instagram</Button>
          </div>
        </div>
      </footer>
    </div>
  );
}
