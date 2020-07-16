# Arc-Flash-Calculator
Designing an arc flash Arcing Current, Incident Energy, and Protection Boundary calculator.

HOW TO RUN THE CODE: 

1) Make sure the Excel files (attached in the repository) are in the same folder as the .m file.

2) Apply the following Code


%% Defining Initial Values
V=  input('Enter voltage in kV ');
Ibf=  input('Enter bolt faulted current in kA ');
G=  input('Enter electrode gap in mm  ');
Wd=  input('Enter working distance in mm ');
arcT=input('Enter arc duration in ms ');
% Determining Arcing current
Iarc_600=10^(0.043785+(1.04*log10(Ibf))+(-0.18*log10(G)))*((0*(Ibf^6))+(0*(Ibf^5))+(-4.786*10^-9*(Ibf^4))+(1.962*10^-6*(Ibf^3))+(-0.000229*(Ibf^2))+(0.003141*Ibf)+1.092);
Iarc_2700=10^(-0.02395+(1.006*log10(Ibf))+(-0.0188*log10(G)))*((-1.557*10^-12*(Ibf^6))+(4.556*10^-10*(Ibf^5))+(-4.186*10^-8*(Ibf^4))+(8.346*10^-7*(Ibf^3))+(5.482*10^-5*(Ibf^2))+(-0.003191*Ibf)+0.9729);
Iarc_14300=10^(0.005371+(1.0102*log10(Ibf))+(-0.029*log10(G)))*((-1.557*10^-12*(Ibf^6))+(4.556*10^-10*(Ibf^5))+(-4.186*10^-8*(Ibf^4))+(8.346*10^-7*(Ibf^3))+(5.482*10^-5*(Ibf^2))+(-0.003191*(Ibf))+0.9729);
if (0.6<V)&&(V<=2.7)    
        Iarc1=(((Iarc_2700-Iarc_600)*(V-2.7))/2.1)+Iarc_2700;
        Iarc2=(((Iarc_14300-Iarc_2700)*(V-14.3))/11.6)+Iarc_14300;
        Iarc3=(Iarc1*((2.7-V)/2.1))+(Iarc2*((V-0.6)/2.1));
        disp('the average arcing current is obtained as= ');
        disp(Iarc3);
        VarCf=(((9.5606*10^-7).*(V^6))+((-5.1543*10^-05).*(V^5))+((0.0011161).*(V^4))+((-0.01242).*(V^3))+((0.075125).*(V^2))+((-0.23584).*(V))+(0.334627));
        Cf=1-(VarCf/2);   
Iarcmin1=(Iarc3*(1-(0.5*VarCf)));
disp('the lower bound arcing current is obtained as= ');
disp(Iarcmin1);
Iarcmin2 = Iarc3*(1-0.5*VarCf);
disp('The lower bound arcing current is obtained as= ');
disp(Iarcmin2)
Iarcmin3 = Iarc2*(1-0.5*VarCf);
disp('The lower bound arcing current is obtained as= ');
disp(Iarcmin3)    
elseif (2.7<V)    
        Iarc2=(((Iarc_14300-Iarc_2700)/11.6)*(V-14.3))+Iarc_14300;
        disp('the average arcing current is obtained as= ');
        disp(Iarc2);
        VarCf=(((9.5606*10^-7).*(V^6))+((-5.1543*10^-05).*(V^5))+((0.0011161).*(V^4))+((-0.01242).*(V^3))+((0.075125).*(V^2))+((-0.23584).*(V))+(0.334627));
        Cf=1-(VarCf/2);   
        Iarcmin1=(Iarc2*(1-(0.5*VarCf)));
        disp('the lower bound arcing current is obtained as= ');
        disp(Iarcmin1);    
elseif (0.208<=V)&&(V<=0.6)   
        Iarc=1/sqrt(((0.6/V).^2).*((1/(Iarc_600^2))-(((0.6^2)-(V^2))/((0.6^2).*(Ibf^2)))));        
        VarCf=(((9.5606*10^-7).*(V^6))+((-5.1543*10^-05).*(V^5))+((0.0011161).*(V^4))+((-0.01242).*(V^3))+((0.075125).*(V^2))+((-0.23584).*(V))+(0.334627));
        Cf=1-(VarCf/2);   
        Iarcmin1=(Iarc*(1-(0.5*VarCf)));
        disp('the lower bound arcing current is obtained as= ');
        disp(Iarcmin1);
        Iarcmin2 = Iarc3*(1-0.5*VarCf);
        disp('The lower bound arcing current is obtained as= ');
        disp(Iarcmin2)
        Iarcmin3 = Iarc2*(1-0.5*VarCf);
        disp('The lower bound arcing current is obtained as= ');
        disp(Iarcmin3)        
end  
for i=1:3
    if(i==1)
       Iarcf(i)=Iarc_600;
    end
    if(i==2)
        Iarcf(i)=Iarc_2700;
    end
    if(i==3)
        Iarcf(i)=Iarc_14300;
    end
end

%% Calculating Incident Energy
for i=1:3
    if(i==1)
        ki1=0.679294;
        ki2=0.746;
        ki3=1.222636;
        ki4=0;
        ki5=0;
        ki6=-4.783*10^-9;
        ki7=0.000001962;
        ki8=-0.000229;
        ki9=0.003141;
        ki10=1.092;
        ki11=0;
        ki12=-1.598;
        ki13=0.997;
    end
    if(i==2)
        ki1=3.880724;
        ki2=0.105;
        ki3=-1.906033;
        ki4=-1.557*10^-12;
        ki5=4.556*10^-10;
        ki6=-4.186*10^-8;
        ki7=8.346*10^-7;
        ki8=5.482*10^-5;
        ki9=-0.003191;
        ki10=0.9729;
        ki11=0;
        ki12=-1.515;
        ki13=1.115;
        end
    if(i==3)
        ki1=3.405454;
        ki2=0.12;
        ki3=-0.93245;
        ki4=-1.557*10^-12;
        ki5=4.556*10^-10;
        ki6=-4.186*10^-8;
        ki7=8.346*10^-7;
        ki8=5.482*10^-5;
        ki9=-0.003191;
        ki10=0.9729;
        ki11=0;
        ki12=-1.534;
        ki13=0.979;
    end
    qw(i)=ki1+ki2*log10(G)+((ki3*Iarcf(i))/((ki4*Ibf^7)+(ki5*Ibf^6)+(ki6*Ibf^5)+(ki7*Ibf^4)+(ki8*Ibf^3)+(ki9*Ibf^2)+(ki10*Ibf)))+(ki11*log10(Ibf))+(ki12*log10(Wd))+(ki13*log10(Iarcf(i)));    
    E(i)=((12.552*arcT)/50)*10^qw(i);
    qwAFB(i)=(ki1+ki2*log10(G)+((ki3*Iarcf(i))/((ki4*Ibf^7)+(ki5*Ibf^6)+(ki6*Ibf^5)+(ki7*Ibf^4)+(ki8*Ibf^3)+(ki9*Ibf^2)+(ki10*Ibf)))+(ki11*log10(Ibf))+(ki13*log10(Iarcf(i)))+log10(1)-log10(20/arcT))/-ki12;
    AFB(i)=10^qwAFB(i);
end
if(V<=0.6)    
        ki1=0.679294;
        ki2=0.746;
        ki3=1.222636;
        ki4=0;
        ki5=0;
        ki6=-4.783*10^-9;
        ki7=0.000001962;
        ki8=-0.000229;
        ki9=0.003141;
        ki10=1.092;
        ki11=0;
        ki12=-1.598;
        ki13=0.997;    
    qw(4)=ki1+ki2*log10(G)+((ki3*Iarcf(1))/((ki4*Ibf^7)+(ki5*Ibf^6)+(ki6*Ibf^5)+(ki7*Ibf^4)+(ki8*Ibf^3)+(ki9*Ibf^2)+(ki10*Ibf)))+(ki11*log10(Ibf))+(ki12*log10(Wd))+(ki13*log10(Iarc)+log10(Cf));    
    E(4)=((12.552*arcT)/50)*10^qw(4);
    disp('The Incident Energy in J/cm2 is obatined as= ');
    disp(E(4));     
    disp('The Incident Energy in cal/cm2 is obtained as= ');
    disp(E(4)/4.184);
    %Arc FLash Boundary is found as for V<0.6
    qwAFB(4)=(ki1+ki2*log10(G)+((ki3*Iarcf(1))/((ki4*Ibf^7)+(ki5*Ibf^6)+(ki6*Ibf^5)+(ki7*Ibf^4)+(ki8*Ibf^3)+(ki9*Ibf^2)+(ki10*Ibf)))+(ki11*log10(Ibf))+(ki13*log10(Iarc))+log10(Cf)-log10(20/arcT))/-ki12;
    AFB(4)=10^qwAFB(4);
    disp('The Arc Flash boundary in mm= ');
    disp(AFB(4));        
elseif (0.6<V)&&(V<=2.7)
    %Incident Energy when V>0.6 && V<2.7
    E1=(((E(2)-E(1))*(V-2.7))/2.1)+E(2);
    E2=(((E(3)-E(2))*(V-14.3))/11.6)+E(3);
    E3=(E1*((2.7-V)/2.1))+(E2*((V-0.6)/2.1));
    disp('The Incident Energy in J/cm2 is obtained as= ');
    disp(E3);
    disp('The Incident Energy in cal/cm2 is obtained as= ');
    disp((E3)/4.184);
    %AFB when V>0.6 && V<2.7
     AFB1=(((AFB(2)-AFB(1))*(V-2.7))/2.1)+AFB(2);
     AFB2=(((AFB(3)-AFB(2))*(V-14.3))/11.6)+AFB(3);
     AFB3=(AFB1*((2.7-V)/2.1))+(AFB2*((V-0.6)/2.1));
     disp('The Arc Flash boundary in mm is obtained as= ');
     disp(AFB3);        
elseif (2.7<V)  
      E2=(((E(3)-E(2))*(V-14.3))/11.6)+E(3);
      disp('The Incident Energy in J/cm2 is obtained as= ');
      disp(E2);
      disp('The Incident Energy in cal/cm2 is obtained as= ');
      disp((E2)/4.184);
      %Arc FLash Boundary when V>2.7
      AFB2=(((AFB(3)-AFB(2))*(V-14.3))/11.6)+AFB(3);
      disp('The Arc Flash boundary in mm is obtained as=');
      disp(AFB2);
end
