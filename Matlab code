function varargout = Marcy(varargin)
gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
                   'gui_Singleton',  gui_Singleton, ...
                   'gui_OpeningFcn', @Marcy_OpeningFcn, ...
                   'gui_OutputFcn',  @Marcy_OutputFcn, ...
                   'gui_LayoutFcn',  [] , ...
                   'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end

if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end

function Marcy_OpeningFcn(hObject, eventdata, handles, varargin)
handles.output = hObject;
guidata(hObject, handles);
set(handles.axes1,'Visible','off');
set(handles.axes2,'Visible','off');
global queimada;
queimada = 0;
pause on;

function varargout = Marcy_OutputFcn(hObject, eventdata, handles) 
varargout{1} = handles.output;

function Open_Callback(hObject, eventdata, handles)%ação de apertar o botão
loop(handles); %chamada da função de repetição

function loop(handles) %função responsavel por carregar mais de uma imagem seguida
x=0;
k=0;
while x==0 
k=k+1;
entrada = "C:\Users\kairo\OneDrive\Área de Trabalho\fotos luzes\capture_"+k+".jpg";%path para as fotos, devendo ser salavs como capture_numero da foto
if isfile(entrada)
handles.arquivo = entrada;
handles.image = imread(entrada);
 axes(handles.axes1);
 imshow(handles.image);
 title('original');
 
aperte2(handles);
pause(3);
else
break;
end
end

function aperte2(handles)
L = 220;
global queimada;
original=handles.image;
if(size(original,3)==3)
    x = rgb2gray(original);
else
    x = original;    
end
bool_img = x < L;
x(bool_img) = 0;
x = medfilt2(x);

queimada = queimada + 1;
saida = "C:\Users\kairo\OneDrive\Área de Trabalho\salvamento automatico\imagem teste"+queimada+".jpeg";
imwrite(x,saida);
%out = imerode(x, strel("square", 5));
out = bwareaopen(x, 110);
info = regionprops(out,'Boundingbox') ;
axes(handles.axes2); 
imshow(original);
comparar(out);
for k = 1 : length(info)
     BB = info(k).BoundingBox;
     roi = drawrectangle('Position',[BB(1),BB(2),BB(3),BB(4)],'Color','r', 'FaceAlpha', 0.1,'LineWidth',1);
end
title('foco de luz');

function comparar(x)
entrada = "C:\Users\kairo\OneDrive\Área de Trabalho\salvamento automatico\referencia.jpeg";
if isfile(entrada)
comp=imread(entrada);
comp2 = im2double(comp)-im2double(x);
out2 = bwmorph(comp2,'clean');
out3 = bwareaopen(out2, 150);
out4 = imerode(out3, strel("square", 25));
info = regionprops(out4,'BoundingBox') ;

for k = 1 : length(info)
     BB = info(k).BoundingBox;
     roi = drawrectangle('Position',[BB(1)+1,BB(2)+1,BB(3)+1,BB(4)+1],'Color','b', 'FaceAlpha', 0.1,'LineWidth',1);
    
end
else
     imwrite(x,entrada);
end


% --------------------------------------------------------------------
function imgweb_Callback(hObject, eventdata, handles)
entrada =  "http://10.13.70.177/savedphoto";
handles.image = imread(entrada, 'jpg');
 axes(handles.axes1);
 imshow(handles.image);
 title('original');
 
aperte2(handles);


