% FDMA
%FDMA matlab code using parameters

clc;
clear all
close all
no=4
t=[0:100]
mf=[30 40 50 60]
fc=[300 600 900 1200];
fdev=10;
for i=1:no
    m(i,:)=sin(2*pi*mf(1,i)*t/1000)+2*sin(pi*4*t/1000)
end;
for i=1:no
    y(i,:)=fmmod(m(i,:),fc(1,i),10*fc(1,i)*10,fdev); 
end
ch_op=awgn(sum(y),20,'measured');
for i=1:no
receiver(i,:)=fmdemod(ch_op,fc(1,i),10*fc(1,i),fdev);
end
C = {'k','b','r','g','y',[.5 .6 .7],[.8 .2 .6],[.3 .2 .2]};%cell  array of colours
for i=1:no
    figure(1)
    hold on
    plot(m(i,:),'color',C{i});
    xlabel('time index');
    ylabel('amplitude');
    title('signal from different users before modulation');
    figure(2)
    hold on
    plot(y(i,:),'color',C{i});
    xlabel('time index');
    ylabel('amplitude');
    title('signal from different users after modulation');
    figure(3)
    plot(ch_op)
    xlabel('time index');
    ylabel('amplitude');
    title('signal after passing through the channel');
    figure(4)
    plot(receiver(i,:),'color',C{i});
    xlabel('time index');
    ylabel('amplitude');
    title('Signal after demodulation');
    
end
figure
pwelch(ch_op,[],[],[],1000);
title('Power Spectral Density Estimate');









