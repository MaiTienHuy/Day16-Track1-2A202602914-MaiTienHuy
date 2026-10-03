# Memo Teardown — Cursor

**Họ tên:** Mai Tiến Huy<br>
**Mã sinh viên:** 2A202602914<br>
**Ngày nghiên cứu:** 03/10/2026

**Vì sao chọn sản phẩm này:** Cursor lấy AI làm trung tâm của việc viết và giao phần việc lập trình; các thay đổi từ editor sang agent rồi sang quy trình giao phần mềm tạo thành một timeline có thể kiểm chứng. Use case chính là giúp người xây phần mềm sửa, hiểu, kiểm tra và đưa thay đổi vào sản phẩm nhanh hơn mà vẫn kiểm soát được kết quả.

## §1. Timeline các cập nhật lớn

*“Nguyên lý” dưới đây là phần suy luận từ quyết định sản phẩm, không phải lời giải thích chính thức của Cursor. Context chỉ nêu điều có thể đối chiếu từ nguồn, tránh gán động cơ chưa được công bố.*

| Thời điểm | Cập nhật | Context lúc đó | Nguyên lý |
|---|---|---|---|
| **03/2023** | [Đưa Cursor ra cộng đồng lập trình](https://news.ycombinator.com/item?id=35285047) như một editor để lập trình cùng AI. Người dùng sớm trong thread nói họ dùng Cursor tạo mã rồi sửa tiếp bằng VS Code. | ChatGPT và VS Code là các công cụ đã có trong quy trình của người dùng sớm; [thảo luận sau đó](https://news.ycombinator.com/item?id=37888477) cho thấy ma sát chép mã giữa chat và editor. | **x10 ở thao tác có tần suất cao:** đặt AI ngay trong chỗ lập trình để rút ngắn vòng “hỏi → chép → sửa”, trước khi tự động hóa toàn quy trình. |
| **08/2024** | [Mở Composer mặc định cho Pro/Business](https://cursor.com/changelog/0-40-x), cho sửa nhiều chỗ bằng một yêu cầu; cùng đợt cải thiện Tab và thử nghiệm chia sẻ chỉ dẫn giữa các Composer. | Một lượt gợi ý Tab chỉ giải quyết phần mã ngay trước mắt; công việc thật thường trải qua nhiều tệp và cần thấy bản sửa để duyệt. | **Định nghĩa lại “tốt” theo việc hoàn tất:** thước đo chuyển từ gợi ý dòng mã đúng sang tạo được thay đổi nhiều tệp mà người dùng xem xét được. |
| **11/2024** | [Đưa Agent vào Composer](https://cursor.com/changelog/0-43-x): phiên bản đầu tự chọn ngữ cảnh và dùng terminal, bên cạnh giao diện diff. | Composer đã nhận yêu cầu nhiều tệp nhưng người dùng vẫn phải tự tìm đủ ngữ cảnh và thực hiện nhiều bước bằng tay. | **Vertical AI = AI Expert + Domain Expert:** năng lực model được gắn với công cụ, cấu trúc repo và vòng chạy lệnh của nghề lập trình; giá trị nằm ở hoàn thành việc trong workflow. |
| **01/2025** | [Thêm `.cursor/rules` và model hiểu codebase](https://cursor.com/changelog/0-45-x): quy tắc cấp repo nằm trên đĩa, agent chọn quy tắc phù hợp. | Khi agent can thiệp nhiều tệp, chỉ dẫn nhập lại trong từng cuộc hội thoại dễ mất; repo khác nhau có chuẩn, lệnh và kiến trúc khác nhau. | **Wrapper → moat từ ngữ cảnh workflow:** quy tắc được lưu cùng repo biến tri thức của nhóm thành đầu vào lặp lại; chỉ gọi một model chung khó tái tạo đúng chuẩn dự án. |
| **06/2025** | [Cursor 1.0 mở Background Agent cho mọi người và ra Bugbot](https://cursor.com/changelog/1-0) để rà lỗi trên pull request. | Agent trong editor đã hỗ trợ tạo mã; bước kế tiếp của công việc là chạy tác vụ khi người viết không ngồi trước máy và kiểm tra thay đổi trước khi nhập nhánh. | **Vòng lặp học “tạo → kiểm → sửa”:** sản phẩm đi theo đơn vị công việc là PR, thêm lớp đánh giá kết quả thay vì chỉ tăng tốc sinh mã. |
| **10/2025** | [Cursor 2.0 ra model Composer riêng và giao diện điều phối tối đa tám agent song song](https://cursor.com/changelog/2-0), mỗi agent có môi trường tách biệt. | Tác vụ agent phức tạp hơn làm chi phí, độ trễ và xung đột chỉnh sửa trở thành vấn đề của sản phẩm; Cursor cũng đã có agent chạy trên cloud. | **Moat ở hệ thống thực thi:** sở hữu model tối ưu cho tác vụ và cơ chế cô lập/điều phối tạo lợi thế ngoài lớp giao diện gọi model. |
| **04/2026** | [Cursor 3 chuyển giao diện chính sang Agents Window](https://cursor.com/changelog/3-0): nhiều agent trên nhiều repo, môi trường local/cloud/SSH; vẫn có thể mở editor. | [Michael Truell ghi nhận](https://cursor.com/blog/third-era) số người dùng Agent đã gấp đôi Tab, đảo chiều so với 03/2025; người dùng phải theo dõi nhiều phiên làm việc cùng lúc. | **Định nghĩa lại “tốt” theo mức kiểm soát:** khi AI viết phần lớn mã, giá trị của sản phẩm chuyển sang giao việc, quan sát và duyệt đầu ra của nhiều agent. |
| **09/2026** | [Ra Rollouts và Security Review](https://cursor.com/changelog/rollouts-and-security-reviewer) cho Teams/Enterprise: theo dõi sức khỏe thay đổi sau deploy và dò lỗ hổng trên PR. | Khối lượng thay đổi do agent tạo có thể vượt khả năng kiểm tra thủ công; Cursor đã có [Projects](https://cursor.com/changelog/projects) điều phối tác vụ dài hạn. | **Định nghĩa “tốt” bằng kết quả an toàn sau phát hành:** vòng lặp học đi từ mã/PR tới tín hiệu production; moat nằm ở kết nối repo, deploy và telemetry. |

**Vì sao chọn những mốc này:** Tám mốc trên đổi *đơn vị công việc* từ dòng mã → sửa nhiều tệp → tác vụ agent → PR → nhiều agent → kết quả sau deploy. [Cursor Tab dự đoán lần sửa kế tiếp (02/2024)](https://www.producthunt.com/products/cursor/launches) và [cải thiện terminal/độ trễ (07/2025)](https://cursor.com/changelog/1-3) được cân nhắc nhưng loại khỏi bảng: chúng làm trải nghiệm hiện có tốt hơn, ít thay đổi phạm vi công việc hay người mua hơn. [Đổi giá Teams 08/2025](https://cursor.com/blog/aug-2025-pricing-teams) và [ghế Premium 06/2026](https://prod.cursor.com/blog/teams-pricing-june-2026) là ứng viên quyết định thương mại thật; bảng dành chỗ cho các mốc làm rõ hơn đường chuyển từ editor sang kiểm chứng sản phẩm.

## §2. Tệp user & JTBD

Hai chân dung dưới đây là **persona suy luận từ nguồn công khai**, không phải số liệu cơ cấu khách hàng. [Thread HN 2023](https://news.ycombinator.com/item?id=37888477) mô tả nhu cầu tránh chép mã giữa ChatGPT và editor; [trang Product Hunt](https://www.producthunt.com/products/cursor/launches) lưu các lần ra mắt; [thông báo Enterprise](https://cursor.com/changelog/enterprise-dec-2025) và [bản Teams/Enterprise 09/2026](https://cursor.com/changelog/rollouts-and-security-reviewer) cho thấy sản phẩm đang phục vụ cả tổ chức lớn.

| | Early adopters | Tệp hiện tại được mở rộng |
|---|---|---|
| **Đặc điểm** | Một lập trình viên làm sản phẩm ở startup nhỏ, quen VS Code, tự thử công cụ AI qua HN/Product Hunt, trực tiếp đọc và sửa từng diff. Đây là chân dung điển hình suy từ thảo luận sớm, không khẳng định mọi người dùng đầu tiên đều như vậy. | Một tech lead hoặc platform engineer ở nhóm có nhiều repo, PR và môi trường deploy; họ giao việc cho nhiều agent, phải duyệt thay đổi, quản lý chi phí và rủi ro của cả nhóm. |
| **JTBD chính** | Hoàn tất một bản sửa hoặc tính năng nhỏ nhanh hơn trong repo đang mở, đồng thời hiểu mã được thêm vào. | Đưa một thay đổi qua chu trình giao việc → tạo mã → review → deploy một cách có thể kiểm soát, đo được lỗi và chi phí. |
| **Trước đó họ làm bằng cách nào** | Viết trực tiếp trong VS Code; tra tài liệu hoặc hỏi ChatGPT rồi chép câu trả lời về editor, chạy/test thủ công. | Chia ticket cho lập trình viên, dùng IDE và CI/CD riêng, review PR bằng mắt, theo dõi deploy qua công cụ telemetry và bảo mật tách rời. |
| **Mốc §1 gây dịch chuyển** | Mốc 03/2023 và 08/2024 giảm chi phí thử một editor mới cho cá nhân. | Mốc 06/2025 (Bugbot/Background Agent) mở rộng khỏi editor; 10/2025 và 04/2026 cho quản lý nhiều agent; 09/2026 đưa kết quả vào quy trình Teams/Enterprise. |

**Dịch chuyển tệp:** Đây là **mở rộng người dùng và người mua**, không có bằng chứng rằng lập trình viên cá nhân đã rời sản phẩm. Chuỗi mốc 06/2025 → 09/2026 khiến người quyết định mua không chỉ hỏi “gợi ý mã nhanh không?” mà còn hỏi “nhóm có kiểm soát được PR, chi phí, quyền truy cập và rủi ro production không?”. Các tính năng Enterprise như billing groups và security controls là bằng chứng về nhu cầu của tổ chức, không phải bằng chứng định lượng về tỷ trọng doanh thu. [Nguồn](https://cursor.com/changelog/enterprise-dec-2025).

**Switching cost theo 4 forces:**

| Lực | Tác động với Cursor |
|---|---|
| **Push — bực với cách cũ** | Chép mã giữa chat và IDE, tự nối ngữ cảnh giữa nhiều tệp, chờ người khác xử lý PR làm người dùng muốn đổi. Thảo luận sớm ghi nhận đúng ma sát chép mã này. [Nguồn](https://news.ycombinator.com/item?id=37888477). |
| **Pull — sức hút của cách mới** | Composer/Agent nhận việc nhiều bước; Teams/Enterprise có review bảo mật và theo dõi deploy trong cùng chu trình. [Nguồn](https://cursor.com/changelog/rollouts-and-security-reviewer). |
| **Habit — thói quen giữ cách cũ** | Phím tắt, extension, cấu hình và quy trình VS Code/GitHub đã quen khiến đổi editor hoặc quy trình review không tức thì. Một [review Product Hunt](https://www.producthunt.com/products/cursor) nêu rõ việc giữ extension/phím tắt là lý do chuyển sang Cursor dễ hơn. |
| **Anxiety — lo lắng khi đổi** | Lo agent sửa sai trên repo lớn, lộ ngữ cảnh, chi phí khó đoán và phải học cách kiểm soát nhiều phiên; [review Product Hunt](https://www.producthunt.com/products/cursor) nêu mất context và giới hạn giá, còn [Cursor đưa ra kiểm soát chi phí cho Teams](https://prod.cursor.com/blog/teams-pricing-june-2026). |

**Lực giữ mạnh nhất:** *Habit được chuyển vào Cursor rồi tích lũy thành ngữ cảnh nhóm*: giao diện gần VS Code giảm cản trở ban đầu; rules, thiết lập nhóm, lịch sử và kết nối repo làm workflow mới trở nên quen. Đây là **suy luận**, không phải moat tuyệt đối: nếu VS Code/GitHub hoặc agent khác có cùng khả năng hiểu repo, kiểm chứng PR và quản trị với chi phí thấp hơn, lực giữ này sẽ yếu đi. Chính phàn nàn về mất context/giá trong review là tín hiệu cho khả năng đó. [Nguồn rules](https://cursor.com/changelog/0-45-x), [nguồn review](https://www.producthunt.com/products/cursor).

## §3. Ba dự đoán hướng đi (04–10/2027)

**Dự đoán 1** *(loại: mở rộng tính năng)*<br>
**Dự đoán:** Cursor sẽ nối Rollouts với feature flag hoặc công cụ deploy để agent đề xuất chặn rollout hay tạo revert PR khi tín hiệu production xấu, nhưng vẫn yêu cầu người có quyền duyệt hành động cuối.<br>
**Lập luận:** Mốc 09/2026 đã theo dõi deploy và [Cursor ghi rõ feature flag là tích hợp sắp tới](https://cursor.com/changelog/rollouts-and-security-reviewer); JTBD của tech lead ở §2 là đưa thay đổi vào production có kiểm soát. Bước tiếp theo hợp logic là biến cảnh báo thành quyết định có thể duyệt.

**Dự đoán 2** *(loại: mở rộng segment)*<br>
**Dự đoán:** Cursor sẽ bán gói/quy trình cho người phụ trách platform hoặc AppSec, với dashboard cấp tổ chức gom kết quả Security Review, Rollouts và chính sách agent theo repo.<br>
**Lập luận:** Mốc 06/2025 thêm review PR, 09/2026 thêm kiểm tra bảo mật và production; tệp ở §2 đã có người chịu trách nhiệm chất lượng toàn nhóm. [Enterprise Insights](https://cursor.com/changelog/enterprise-dec-2025) cho thấy Cursor đã xây bề mặt quản trị để phục vụ họ.

**Dự đoán 3** *(loại: thay đổi mô hình kiếm tiền)*<br>
**Dự đoán:** Cursor sẽ đưa ra hạn mức/giá riêng cho các bot kiểm chứng theo số PR hoặc lần deploy được xử lý, bên cạnh phí ghế và lượng dùng agent.<br>
**Lập luận:** Mốc 09/2026 đưa thêm tác vụ Rollouts/Security Review cho Teams/Enterprise; JTBD của người mua ở §2 đòi chi phí dự báo được. Cursor đã [chuyển Teams sang giá theo usage năm 2025](https://cursor.com/blog/aug-2025-pricing-teams) và [tách ghế Standard/Premium năm 2026](https://prod.cursor.com/blog/teams-pricing-june-2026), nên đơn vị giá theo công việc kiểm chứng là một phép thử hợp lý.

**Dự đoán tự tin nhất:** số 1, vì tích hợp feature flag đã được Cursor công khai nêu là bước tới. **Giả định có thể làm nó gãy:** khách hàng không cho agent đụng vào quy trình deploy hoặc telemetry không đủ tin cậy để đề xuất chặn/revert. Đây là dự đoán tại ngày 03/10/2026, không phải thông báo sản phẩm đã ra mắt.

## §4. AI Log

| Việc | AI làm hay bạn làm? | Kiểm chứng/phán đoán lại thế nào? |
|---|---|---|
| Gom nguồn và dựng danh sách mốc ứng viên | AI trợ lý thực hiện. | AI đã mở trực tiếp trang HN, Product Hunt, các changelog Cursor và bài founder; danh sách nguồn thô nằm trong `research-notes.md`. Người nộp chưa trực tiếp xác nhận lại từng link. |
| Chọn tám mốc và đối chiếu ngày/tính năng | AI trợ lý đề xuất và viết. | Đối chiếu ngày và nội dung từng hàng với link gốc ngay trong bảng; phân biệt mốc ra tính năng với bản vá. Người nộp cần tự đọc lại trước khi bảo vệ bài. |
| Gắn nguyên lý, dựng persona và 4 forces | AI trợ lý phân tích. | Đánh dấu rõ đâu là dữ kiện nguồn, đâu là suy luận; dùng review có phàn nàn để thử phản biện giả thuyết moat. Đây chưa phải nghiên cứu người dùng trực tiếp. |
| Viết ba dự đoán và memo | AI trợ lý soạn bản nộp; chưa có phán đoán độc lập của người nộp trong cuộc trao đổi này. | Mỗi lập luận trỏ về mốc §1/tệp §2, nêu điều kiện làm dự đoán gãy; người nộp nên tự kiểm tra và chỉnh nhận định trước khi nộp như bài cá nhân. |
