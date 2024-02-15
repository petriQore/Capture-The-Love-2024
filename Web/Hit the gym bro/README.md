![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/9e46b912-9279-4d28-883c-b87b9f0210c2)

upon visiting the website, we're met with this login page where we have the option to either sign up or login:

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/1b2a1226-fa45-4e5c-b4f6-970e5d188fbe)

let's try logging in with admin admin:

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/ec4e621a-1a42-4d85-9714-344bc185f0f0)

hmm we should probably sign up first:

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/0e932d92-602f-4bc5-8924-a6bb51521e94)

after signing up and trying to login again we're met with this message, let's check the cookies for this token.

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/5620760e-5f18-4f4e-8265-38b4c4b19412)

this looks like a ```JSON Web Token``` or ```JWT``` for short, let's decode it to check its contents, you can use this website: [JWT Decode](https://jwt.io)

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/87eaf793-fcc7-4038-a17e-6bdedba56dbf)

test was the username i signed up with, and we can see that it has the role of user, what if we can change this role to admin ??
first, we would have to find out the secret key that the jwt was signed with, then we could craft our modified data, sign the token with the same key and use it to gain access.

there is a tool called [jwt-cracker](https://github.com/lmammino/jwt-cracker) that can find out the key with the help of a dictionary, we can use rockyou.txt for that:

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/af7a6362-2b7f-4d44-8704-c13f046ecd2d)

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/95dd8a6f-cc1f-4491-984d-2932f89f633b)

oops! it seems that this solution wasn't the right one after all. we have to come up with something else.

after looking around online for a while i found out that we can actually change the algorithm used to sign the token to ```none``` and in that case, we won't need the last part of the token, we can just leave it empty.
knowing that, we can manually craft each part of the token, encode them to base64 and just combine the parts at the end:

# First part:

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/ee825838-9656-426e-b16c-660ccab66c53)

# Second part:

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/3af64084-d82a-4721-bf16-47e459f16c3f)

so my final token becomes: ```eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJ1c2VybmFtZSI6InRlc3QiLCJyb2xlIjoiYWRtaW4iLCJpYXQiOjE3MDgwMjMwMzd9.```

let's try logging in now

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/8e72443d-b149-48a9-8013-eb7fbee0ef11)

we're in!!!

but it seems we aren't done yet, we have some forms where we can edit the profile, but none of them worked.
however if we quickly check the url: ```http://51.12.211.165:8500/app/user``` <br>
hmmm what if i change the ```user``` to ```admin```, it should work since we changed the role value to admin earlier, right ??

![image](https://github.com/petriQore/Capture-The-Love/assets/123587287/95921277-0a13-4020-9fcf-2f89a35489bd)

nice!

flag: ```securintes{35c4p3_d1llu510n5_637_600d}```
