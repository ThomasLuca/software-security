# Top Design Flaws

Top 10 design flaws according to IEEE Center for Secure Design

1. Assume trust, rather than give it or award it
2. Use an auth mechanism that can be bypassed
3. Authorize w/o considering sufficient context
4. Confuse data and control instructions from untrusted sources
5. Fail to validate data
6. Fail to use cryptography correctly
7. Fail to identify sensitive data
8. Ignore the users
9. Integrate external components w/o considering their attack surface
10. Rigidly constrain future changes to objects and actors

## Auth bypass

1. Mobile apps use __SSL behind the scenes__, meaning that the app will not prompt the user when getting invalid SSL certificate.  
This problem mostly occurs in mobile apps because devs disable the feature to test & develop more easily. __Security is not a feature!__

2. __Auth tokens with long timeouts__ tokens with long timeouts motivate brute-force attempts (to short timeouts are bad for user experience)

## Bad Crypto

It's apparently very hard to develop a good crypto system. Therefor it's recommended to use a good community build crypto algorithm.

Also don't trust crypto system to much. Encryption can be tampered with and hash can't protect confidentiality.

Use properly generated keys with large size and protect the keys from compromise.

## Ignore which data is sensitive

eg: Apple ignored users geolocation in IOS (2012) as sensitive data.
