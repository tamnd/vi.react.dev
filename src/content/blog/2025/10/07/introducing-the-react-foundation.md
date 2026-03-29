---
title: "Giới thiệu React Foundation"
author: Seth Webster, Matt Carroll, Joe Savona
date: 2025/10/07
description: Hôm nay, chúng tôi công bố kế hoạch thành lập React Foundation và một cấu trúc quản trị kỹ thuật mới.
---

Ngày 7 tháng 10 năm 2025 bởi [Seth Webster](https://x.com/sethwebster), [Matt Carroll](https://x.com/mattcarrollcode), [Joe Savona](https://x.com/en_JS), [Sophie Alpert](https://x.com/sophiebits)

---


<div style={{display: 'flex', justifyContent: 'center', marginBottom: '1rem', marginLeft: '7rem', marginRight: '7rem' }}>
  <picture >
      <source srcset="/images/blog/react-foundation/react_foundation_logo.png" />
      <img className="w-full light-image" src="/images/blog/react-foundation/react_foundation_logo.webp" />
  </picture>
  <picture >
      <source srcset="/images/blog/react-foundation/react_foundation_logo_dark.png" />
      <img className="w-full dark-image" src="/images/blog/react-foundation/react_foundation_logo_dark.webp" />
  </picture>
</div>

<Intro>

Hôm nay, chúng tôi công bố kế hoạch thành lập React Foundation và một cấu trúc quản trị kỹ thuật mới.

</Intro>

---

Chúng tôi đã mã nguồn mở React từ hơn một thập kỷ trước để giúp các nhà phát triển xây dựng trải nghiệm người dùng tuyệt vời. Ngay từ những ngày đầu, React đã nhận được nhiều đóng góp đáng kể từ các cộng tác viên bên ngoài Meta. Theo thời gian, số lượng người đóng góp và phạm vi đóng góp của họ đã tăng lên rõ rệt. Điều khởi đầu là một công cụ được phát triển cho Meta nay đã mở rộng thành một dự án trải dài qua nhiều công ty với những đóng góp thường xuyên từ khắp hệ sinh thái. React đã vượt ra khỏi khuôn khổ của bất kỳ một công ty nào.

Để phục vụ cộng đồng React tốt hơn, chúng tôi công bố kế hoạch chuyển React và React Native từ Meta sang một React Foundation mới. Là một phần của thay đổi này, chúng tôi cũng sẽ triển khai một cấu trúc quản trị kỹ thuật độc lập mới. Chúng tôi tin rằng những thay đổi này sẽ giúp chúng tôi có thể dành thêm nguồn lực cho các dự án trong hệ sinh thái React.

## The React Foundation {/*the-react-foundation*/}

Chúng tôi sẽ biến React Foundation thành ngôi nhà mới của React, React Native và một số dự án hỗ trợ như JSX. Sứ mệnh của React Foundation sẽ là hỗ trợ cộng đồng và hệ sinh thái React. Khi được triển khai, React Foundation sẽ

* Duy trì hạ tầng của React như GitHub, CI và nhãn hiệu
* Tổ chức React Conf
* Tạo ra các sáng kiến hỗ trợ hệ sinh thái React như hỗ trợ tài chính cho các dự án trong hệ sinh thái, cấp tài trợ và xây dựng chương trình

React Foundation sẽ được điều hành bởi một hội đồng quản trị, với Seth Webster giữ vai trò giám đốc điều hành. Hội đồng này sẽ định hướng nguồn quỹ và tài nguyên để hỗ trợ sự phát triển, cộng đồng và hệ sinh thái của React. Chúng tôi tin rằng đây là cấu trúc tốt nhất để bảo đảm React Foundation giữ được tính trung lập với nhà cung cấp và phản ánh lợi ích tốt nhất của cộng đồng.

Các thành viên doanh nghiệp sáng lập của React Foundation sẽ là Amazon, Callstack, Expo, Meta, Microsoft, Software Mansion và Vercel. Những công ty này đã có ảnh hưởng lớn tới hệ sinh thái React và React Native, và chúng tôi biết ơn sự hỗ trợ của họ. Chúng tôi rất mong được chào đón thêm nhiều thành viên hơn nữa trong tương lai.

<div style={{display: 'flex', justifyContent: 'center', margin: '2rem'}}>
  <picture >
      <source srcset="/images/blog/react-foundation/react_foundation_member_logos.png" />
      <img className="w-full light-image" src="/images/blog/react-foundation/react_foundation_member_logos.webp" />
  </picture>
  <picture >
      <source srcset="/images/blog/react-foundation/react_foundation_member_logos_dark.png" />
      <img className="w-full dark-image" src="/images/blog/react-foundation/react_foundation_member_logos_dark.webp" />
  </picture>
</div>

## Quản trị kỹ thuật của React {/*reacts-technical-governance*/}

Chúng tôi tin rằng định hướng kỹ thuật của React nên được quyết định bởi những người đóng góp và duy trì React. Khi React chuyển sang một foundation, điều quan trọng là không một công ty hay tổ chức nào được đại diện quá mức. Để đạt được điều đó, chúng tôi dự định xác định một cấu trúc quản trị kỹ thuật mới cho React, độc lập với React Foundation.

Trong quá trình xây dựng cấu trúc quản trị kỹ thuật mới của React, chúng tôi sẽ tìm đến cộng đồng để nhận phản hồi. Khi hoàn tất, chúng tôi sẽ chia sẻ chi tiết trong một bài viết sau.

## Cảm ơn {/*thank-you*/}

Sự phát triển đáng kinh ngạc của React là nhờ hàng nghìn con người, công ty và dự án đã góp phần định hình React. Việc tạo ra React Foundation là minh chứng cho sức mạnh và sức sống của cộng đồng React. Cùng nhau, React Foundation và cấu trúc quản trị kỹ thuật mới của React sẽ bảo đảm tương lai của React được vững chắc trong nhiều năm tới.
