unit UQuranku;

{$mode delphi}

interface

uses
  Classes, SysUtils, extjsjson, FileUtil, Forms, Controls, Graphics, Dialogs,
  StdCtrls, ExtCtrls,  fpjson, jsonparser,fphttpclient,LazUTF8;
{ TFrm_Main }

type
  TFrm_Main = class(TForm)
    ListBox1: TListBox;
    Memo1: TMemo;
    procedure FormCreate(Sender: TObject);
    procedure ListBox1Click(Sender: TObject);
    procedure Memo1Change(Sender: TObject);

  private
    { private declarations }
  public
    { public declarations }
  end;

var
  Frm_Main: TFrm_Main;
  JDaftarSurat : TJSONData;

implementation

{$R *.lfm}

{ TFrm_Main }



procedure TFrm_Main.FormCreate(Sender: TObject);
var i:Integer;
begin
    ListBox1.Items.Clear;
    JDaftarSurat := GetJSON(TFPHTTPClient.SimpleGet('http://quranku.xyz/services/DaftarSurat'));
    for i:=0 to JDaftarSurat.Count-1 do
    begin
      ListBox1.Items.Add(JDaftarSurat.Items[i].FindPath('surat_indonesia').AsString+' ( '+JDaftarSurat.Items[i].FindPath('jumlah_ayat').AsString+' Ayat ) ');

    end;



end;

procedure TFrm_Main.ListBox1Click(Sender: TObject);
var JData: TJSONData;i,Ayat,Surat:integer;
begin
    Memo1.Lines.Clear;
    Surat:= ListBox1.ItemIndex+1;
    Ayat:= (JDaftarSurat.Items[ListBox1.ItemIndex].FindPath('jumlah_ayat').AsInteger);
    JData := GetJSON(TFPHTTPClient.SimpleGet('http://quranku.xyz/services/Surah?SuraID='+IntToStr(Surat)));
    Memo1.Lines.BeginUpdate;

    for i := 0 to Ayat-1 do
    begin
      Memo1.Lines.Add(inttostr(i+1));
      Memo1.Lines.Add(Jdata.Items[i].FindPath('AyahText').AsString);
      Memo1.Lines.Add(Jdata.Items[i].FindPath('terjemahan').AsString);
      Memo1.Lines.Add('');

    end;
    Memo1.Lines.EndUpdate;




end;

procedure TFrm_Main.Memo1Change(Sender: TObject);
begin

end;



end.

