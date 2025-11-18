Blog:
Question - ১️ Interfaces এবং Types-এর মধ্যে পার্থক্য — TypeScript-এ

TypeScript-এ interface এবং type alias—দুটোই কোনো object-এর structure বা shape নির্ধারণ করতে ব্যবহৃত হয়। কাজ কাছাকাছি হলেও এদের মধ্যে কিছু গুরুত্বপূর্ণ পার্থক্য আছে। নিচে সেই মূল পার্থক্যগুলো ব্যাখ্যা করা হলো:

 ১. Extending (বাড়ানো) করার নিয়ম

interface সহজেই বহু interface কে extend করতে পারে।

type extend করতে পারে, তবে union/intersection ব্যবহার করতে হয়।

উদাহরণ:

interface A { name: string; }
interface B extends A { age: number; }

type X = { name: string; }
type Y = X & { age: number; }

 ২. Declaration Merging

interface বারবার ঘোষণা করলেও TypeScript সেগুলো merge করে একটিতে পরিণত করে।

type কখনো merge হয় না। একবার ঘোষণা করলে পুনরায় ঘোষণা করা যায় না।

উদাহরণ:

interface User { name: string; }
interface User { age: number; } 
// Final interface = { name: string; age: number; }

 ৩. Object Structure vs Complex Types

interface মূলত object এবং class–এর structure তৈরির জন্য বেশি ব্যবহৃত হয়।

type শুধু object–ই নয়, বরং union, intersection, tuple, function type—সবকিছু define করতে পারে।

 ৪. Class Implements করার ক্ষেত্রে

interface class দ্বারা implement করার জন্য আদর্শ।

যদিও type দিয়েও করা যায়, তবে interface এই ক্ষেত্রে বেশি standard.
 
 
যেখানে object–based structure দরকার, সেখানে interface। আর complex type বা flexibility চাইলে type ব্যবহার করাই ভালো।






Question-২ any, unknown এবং never এর পার্থক্য — TypeScript-এ

TypeScript-এ এই তিনটি টাইপ দেখতে একইরকম মনে হলেও, এগুলোর ব্যবহার সম্পূর্ণ আলাদা। ভুল বোঝার কারণে অনেকেই এগুলো ভুল জায়গায় ব্যবহার করে থাকে।

 ১. any — পুরো TypeScript সিস্টেমকে বাইপাস করে

any মানে হচ্ছে TypeScript আপনার ভেরিয়েবলের উপর কোনো চেকই করবে না।

let value: any = 10;
value = "Hello";
value = true; 


 যখন any ব্যবহার করবেন, তখন আপনি TypeScript-এর সুবিধা হারিয়ে ফেলছেন। তাই ভুল না হলে এটা এড়িয়ে যাওয়া উচিত।

 ২. unknown — নিরাপদ any

unknown সবকিছুই accept করে কিন্তু ব্যবহার করার আগে TypeScript আপনাকে type check করতে বাধ্য করে।

let data: unknown = "Hello";

data.toUpperCase(); //  Error

if (typeof data === "string") {
    data.toUpperCase(); //  Safe
}


 অর্থাৎ unknown হচ্ছে safe alternative to any.

 ৩. never — এমন কিছু যা কখনো ঘটে না

never টাইপ ব্যবহার হয় এমন পরিস্থিতিতে যেখানে কোনো function কোনো value কখনো return করবে না।

function throwError(message: string): never {
    throw new Error(message);
}

