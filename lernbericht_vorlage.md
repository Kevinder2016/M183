# Lern-Bericht
von Kevin Frühwirth

## Einleitung

Das Modul 183 erklärt, wie Sie Ihre Website sichern können und Sicherheitslücken zu minimieren. Dieser Lernbericht erklärt, wie Sie Ihre Website vor SQL-Injection-Angriffen schützen.

## Was habe ich gelernt?

In diesem Projekt habe ich gelernt, wie man PreparedStatements verwendet, um SQL-Interpreter-Injektionen abzufangen und so Websites davor zu schützen.

## Beschreibung
Falscher Code der in der Insecure App war (nicht sicher)

 
        public int insert(News news) {
        final String sql = "INSERT INTO news (posted, header, detail, author, is_admin_news) VALUES ('" + new java.sql.Timestamp(news.getPosted().getTime()) + "','" +          news.getHeader() + "','" + news.getDetail() + "','" + news.getAuthor() + "'," + (news.getIsAdminNews() ? "1" : "0") + ")";
        int id = 0;

        try (Statement stmt = DbAccess.getConnection().createStatement()) {
            stmt.execute(sql);
            id = stmt.getGeneratedKeys().getInt(1);
        } catch (SQLException e) {
            Logger.getLogger(NewsDAO.class.getName()).log(Level.SEVERE, null, e);
        }

        return id;

    }

Die Sicherheitslücke im obigen Codeabschnitt besteht darin, dass Sie sich als Administrator anzeigen lassen können, indem Sie einfach den Eingabewert manipulieren. Das ist hier natürlich harmlos und ändert nur die Farbe der Nachrichtenanzeige, aber wenn das auf einer echten Seite der Fall wäre, könnten dies grosse Folgen haben. Um den Benutzer in diesem Fall als Administrator anzuzeigen, müssen Sie das Eingabefeld auf der News-Page anpassen und folgendes hineinschreiben:

## Verifikation

✍️ Erklären Sie kurz und bündig, inwiefern die von Ihnen verwendeten Medien zeigen, was Sie gelernt haben.

# Reflektion zum Arbeitsprozess

👍 Überlegen Sie sich jeweils etwas, was gut an Ihrer Arbeit lief; 

👎 und etwas, was nicht gut lief.

**VBV**: ✍️ Formulieren Sie davon ausgehend einen *handelbaren* Verbesserungsvorschlag.
